# Problem Set 2

## 1. Concept Questions

 1. **Contexts**. *What are contexts for, and what will be the context for the URL shortening app?*
    1. When creating nonrepetitious values, you don't need everything in existance to not overlap. Rather within specific domains is when you only would care about the overlap, and that is why we pass in the contexts.
    2. For the URL shortening app the contexts would be the shortUrlBase that is passed in. This is because for NonceGeneraration it doesn't matter if mit.edu and youtube.com are given the same suffix, as with URLs the base automatically distinguishes them.

 2. **Storing Used Strings**. *Why must the NonceGeneration store sets of used strings?*
    1. It must store different sets (one for each Context) that way it can keep track of which strings each Context has used.
    2. This storage must be sets of strings for NonceGeneration as it has no clue what types it will be storing. This abstraction is important as it allows the concept to be used in a greater variety of use cases.

 3. **Words as Nonces**. *What about common dictionary words for shortenings. Pros/cons? How to implement?*
    1. Pro: For NonceGeneration use cases that require people to remember the nonce generation, the dictionary words makes it much simpler to remember than a random array of characters.
    2. Con: NonceGeneration doesn't abstract to as many use cases. What if not enough common words? What if hard things to remember is what the consumer wanted from the concept? May help UrlShortening, but for other uses it might not help.
    3. I wouldn't modify NonceGeneration to realize this idea, but rather create a new concept called CommonWordNonceGeneration. For this new concept I would have it store a set of all common dictionary words that it can select from, and have the generate() actions reference it.

## 2. Synchronization Questions

 1. **Partial Matching**. *Why different arguments for the different syncs?*
    1. One possible answer could be if a user wants to shorten the URL with an optional target URL.
    2. Another answer would be that the two seperate syncs have two seperate goals. The generate only wants to generate a valid suffix for the baseUrl, while the register would like to create the vaild shortened URL which can then be used.

 2. **Omitting Names**. *Why isn't omitting names used in every case?*
    1. Clarity or emphasis. Sometimes we may want to stress something that omitting the names woulnd't allows us to do.

 3. **Inclusion of Request**. *Why is request in the first two syncs but not the third?*
    1. Calling an expiration setting action should only be called when we are certain that the resource has been created. This is why we only set the expiration when the Url was generated and then successfully registered before adding the expiration, not just for a request.

 4. **Fixed Domain**. *How to modify synchronizations for fixed domain names?*
    1. No longer need to pass in shortUrlBase, so essentially remove it from all action parameters as it can be assumed to be the only domain we are providing (like 'bit.ly').

 5. **Adding a sync**. *Create a synchronization for resource expiration.*\
      **sync** deleteAfterExpiration\
      **when** ExpiringResource.expireResource () : (resource)\
      **then** UrlShortening.delete (shortUrl: resource)

## 3. Extending The Design

### 3.1 Additional Concepts

**concept** PasswordAuthentication\
**purpose** limit access to known users\
**principle** after a user registers with a username and a password,
they can authenticate with that same username and password
and be treated each time as the same user\
**state**  
    a set of Users with\
        a username String\
        a password String\
        an email String\
**actions**\
    register (username: String, password: String, email: String): (user: User, token: String)\
            **requires** no User exists with username\
            **effects** creates new User with confirmed set to false\
    authenticate (username: String, password: String): (user: User)\
            **requires** User exists with that username and password\
            **effects** they are authenticated as the returned User and able to view other concepts data as that User\

**concept** Analytics [User, Resource]\
**purpose** provide usage metrics\
**principle** user registeres resource and can then view its historical usage\
**state**  
    a set of Trackers with\
        an owner User\
        a usageCount Integer // only visible by owner\
        a targetResource Resource\
**actions**\
    startTracking (user: User, targetResource: Resource)\
            **requires** user owns targetResource and targetResource isn't already being tracked\
            **effects** resource analytics starts being tracked\
    addUsage (targetResource: Resource)\
            **requires** targetResource must currently be tracked\
            **effects** increase targetResource count by one\
    stopTracking (user:User, targetResource: Resource)\
            **requires** user must be owner of targetResource and targetResource must be currently tracked\
            **effects** no longer tracking analytics for resource

**Note:** Resource is an all encompassing concept that captures everything that may want to be tracked, including the UrlShortenings. addUsage() must be synchronized with the Resource's concept.

### 3.2 Synchronizations

      **sync** shorteningCreation\
      **when**\
           PasswordAuthentication.authenticate(username, password: String): (user)\
           UrlShortening.register (): (shortUrl)\
      **then** Analytics.startTracking(user, targetResource: shortUrl)\

      **sync** urlTargetting\
      **when** UrlShortening.lookup (shortUrl) : ()\
      **then** Analytics.addUsage (targetResource: shortUrl)

      **sync** examineAnalytics\
      **when**\
           PasswordAuthentication.authenticate(username, password: String): (user)\
           UrlShortening.register (): (shortUrl) // Left to show this user registered this shortUrl\
           Request.viewAnalytics (currentUser: user, tracker: shortUrl)\
      **where** Analytics concept associates usage with shortUrl\
      **then** Request.response (analytics: usage)

### 3.3 Assess Modularity

- **Allowing users to choose their own short URLS:**
  - Another action would need to be added to the UrlShortening that allows users to provide what they want (sort of like adding an optional parameter). The effect of this action would then depend on whether what they desired has already been used or not.
  - A request to attempt using their short URL would be done first, and if possible then you can fully register it.

- **Using the "word as nonce" strategy:**
  - We would need to modify the NonceGeneration concept to include a base set of common words. When generating nonce action it should try using from this set.
  - Doesn't have to be 100%, if the Context runs out of common words it can default to the previous method.

- **Including the target URL in analytics:**
  - No. Different people may have different shortUrl's associated with the same targetUrl, and the assignment previously said we only wanted the original owner of the shortUrl to view their own data.

- **Generate short URLs that are not easily guessed:**
  - Doesn't make sense? For the purpose of our concept we want something that can be easily remembered, and if it can't be easily guessed you won't be able to easily remember it.

- **Supporting reporting of analytics to non-user registered short URL creators:**
  - Undesirable as this would allow really anyone to view the analytics of any shortUrl that wasn't created by a registered user.
