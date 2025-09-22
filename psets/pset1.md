# Problem Set 1

## 1. Excercise 1

 1. **Invariants**. *What are two invariants of the state?*
    1. Count for an Item within a Request must be nonnegative.
    2. All Purchases must be associated with a Request.
    3. In my opinion the second invariant is more important as the whole point of the GiftRegistration concept is to buy gifts that the owner User wants. If there are purchases that don't fall under Requests then those are gifts the owner didn't want. The purchase action is most affected by it as it must keep track that Purchases are buying for pre registered Items, and it does this by the *"requires Registry exists..."* clause.

 2. **Fixing an action**. *Can you identify an action that breaks this important invariant?*
    1. removeItem currently could break the invariant as it will *"remove the request from the Registry"*, irregardless if a Purchase has already been made for that item.
    2. This problem could be fixed by adding to the removeItem action's requirement to verify that the item does not already have associated Purchases for it.

 3. **Inferring behavior**. *By reading the specs of the concept actions, should a Registry be allowed to open and close repeatedly?*
    1. The open/close actions only require that the Registry is active/inactive respectively, therefore allowing to open and close the Registry several times.
    2. A reason to allow this is if owner Users may want to close the Registry temporarily while they are adding more Requests, and then reopen it whenever they are done.

 4. **Registry deletion**. *There is no action to delete a Registry. Would this matter in practice?*
    1. It could matter if an owner User doesn't want the Registry anymore, irregardless if it is open/closed.
    2. Potential storage implications for Registrys that can pile up and never be deleted.

 5. **Queries**. *What are two common queries likely to be executed against the concept state?*
    1. Registry owner query: List of gifts already purchased.
    2. Giver of a gift query: List of remaining possible gifts and their associated counts.

 6. **Hiding purchases**. *How would you augment the concept specification to support Registry owner surprises?*
    1. Modify state to include "a surprise Flag" for each one of the Registrys.
    2. Add to set of Purchases that they're only visible to owner if "surprise Flag" is false.

 7. **Generic types**. *The User and Item types are specified as generic parameters. Why is this preferable?*
    1. Because defining *things* is complicated! I could want a boat, a dog, a house, or any random list of things in my Registry.
    2. It is better to reduce complexity of the GiftRegistration concept by having a different Item concept and passing it in.

## 2. Excercise 2

**concept** PasswordAuthentication\
**purpose** limit access to known users\
**principle** after a user registers with a username and a password,
they can authenticate with that same username and password
and be treated each time as the same user/
**state**  
    a set of Users with\
        a confirmed Flag\
        a token String\
        a username String\
        a password String\
        an email String\
**actions**\
    register (username: String, password: String, email: String): (user: User, token: String)\
            **requires** no User exists with username\
            **effects** creates new User with confirmed set to false, synchronized w/ other concept to email token to User\
    authenticate (username: String, password: String): (user: User)\
            **requires** User exists with that username and password, AND their confirmed Flag is set to true\
            **effects** they are authenticated as the returned User and able to view other concepts data as that User\
    confirm (username: String, token: String)\
            **requires** User exists with that username and their confirmed Flag is false\
            **effects** User's confirmed Flag set to true

3) *What essential invariant must hold on the state? How is it preserved?*
  To me, the most important invariant is that there should be NO duplicate username in the set of users. This is preserved within the register action, as it verifies no User already exists with that username before registering the new User.

## 3. Excercise 3

**concept** PersonalAccessToken [Scope, Date]\
**purpose** grant non-modifying access to registered user accounts\
**principle** after a user registers with a username and a password,
they can create a personal access token that allows others to access a subset
of their account scopes without modifying what the user can actually access\
**state**\
    a set of Users with\
        a username String\
        a password String\
        a set of Tokens\
        a set of Scopes\
    a set of Tokens with\
        a name String\
        an expiration Date\
        a set of Scopes // token signins only can view scopes defined in their token\
  **actions**\
    register (username: String, password: String): (user: User)\
            **requires** no User exists with username\
            **effects** creates new User\
    authenticate (username: String, password: String): (user: User)\
            **requires** User exists with that username and password, OR valid token exists within that username with that token password\
            **effects** they are authenticated as the User and only capable of accessing resources defined in their set of Scopes\
    generateToken (username: String, password: String, name: String, expiration: String, scopes: Scopes)\
            **requires** User exists with that username and password (ie User owner not Token), AND no token exists in that username with 'name'\
            **effects** new Token added to set of Tokens for User

**Note**: The PersonalAccessToken concept differs from PasswordAuthentication in one main factor, it allows people to grant other people access to a subset of their Scopes. Best explained via example (little long, optional example):\
        **Ex**: Organization MIT has three departments: CS, Math, and Humanities who have a shared group of necessary resources, but each also have department specific resources. With PersonalAccessToken concept we can have one MIT User that creates three distinct personal access tokens that define the necessary scopes for each department (easy, central, and configurable in one account by MIT). On the other hand with PasswordAuthentication we would need 4 different accounts (MIT, MIT-CS, MIT-Math, MIT-Humanities) and configure everything from each one of those accounts. Very similar concepts, but very different end user experience.

**Change GitHub Documentation**: The best way to avoid confusion would to have an explicit section explaining (with an example like above) the differences between the two concepts, as they are so similar. That way they are able to accomidate more of the wide variety of user experiences/knowledge.

## 4. Excercise 4

### 4.1 URL Shortener

**concept** UrlShortener [URL]\
**purpose** shorten URLs\
**principle** someone has URL that is difficult share and can use the provided shorter URL for ease of exchange\
**state**\
    a set of URLs\
        an original URL String\
        a shortened URL String\
        an expiration Date\
  **actions**\
    shortenURL (original: String, desired: String): (shortenedURL: URL)\
            **requires** no non-expired shortened URL exists with desired URL \
            **effects** creates new shortened URL with desired URL, with 24 hour expiration\
    shortenURL (original: String): (shortenedURL: URL)\
            **effects** creates new shortened URL with autogenerated URL suffix and 24 hour expiration\
    deleteShortURL (original: String, shortened: String)\
            **requires** shortened URL must exist with specified original URL AND be expired\
            **effects** removes shortened URL from the state

**Note**: This concept would synchronously work with an automatic scheduler concept to delete the URLs once expired via the deleteShortURL action.

### 4.2 Conference Room Booking

**concept** RoomBooking [Room, User]\
**purpose** allow room reservations\
**principle** someone decides they need a room for an arbitrary event and reserve a room in advance that satisfies their size and time needs\
**state**\
    a set of Openings with\
        an owner User\
        a Room\
        a 24-hour start time Integer\
        a 24-hours end time Integer\
        a MM-DD-YY date String\
        a set of Bookings\
    a set of Bookings with\
        a set of Users // owners\
        an associated Room\
        a 24-hour start time Integer\
        a 24-hour end time Integer\
        a MM-DD-YY date String\
**actions**\
    addOpening (user: User, startTime: String, endTime: String, room: Room, date: String)\
            **requires** no opening exists for that room in specified date/time range\
            **effects** Opening created ready for reservation\
    removeOpening (user: User, startTime: String, endTime: String, room: Room, date: String)\
            **requires** Opening exists with specified parameters, user is owner of said Opening, Opening has no Bookings\
            **effects** Opening removed from set of Openings\
    addBooking (user: User, startTime: String, endTime: String, date: String, room: Room)\
            **requires** an opening exists for specified room/date/time AND doesn't  have any time overlap with existing Bookings\
            **effects** Adds Booking to the set of Bookings for that Opening\
    removeBooking (user: User, startTime: String, endTime: String, date: String, room: Room)\
            **requires** Booking exists with specified parameters, User is owner of said Booking\
            **effects** Booking removed from set of Bookings in Opening

**Note**: The Room concept that is passed in will contain all of the necessary identifying information like building, room number, and capacity that is necessary. Simply better to not overcomplicate this concept with something that could be its own.

### 4.3 Time-Based One-Time Password (TOTP)

**concept** TimeBasedOneTimePassword [User]\
**purpose** double factor authentication\
**principle** after a User logs in with their regular username and password, a one-time shortly lived password will be synchronously sent to them via email. Once received the User can finish logging in with said password.\
**state**\
    a set of OneTimePasswords with\
        an associated User\
        an strong Password\
        an expiration Date\
  **actions**\
    createOneTimePassword (user: User):\
            **requires** User doesn't have active OneTimePassword\
            **effects** creates new OneTimePassword for User with strong cryptographic password generation // synchronized via email concept to send to User\
    authenticate (user: User, password: String): (user: User)\
            **requires** User has active OneTimePassword AND is correct password\
            **effects** Synchronized via other concepts User will have access to their resources\
    deleteOneTimePassword (user: User) // synchronized via scheduler concept\
            **requires** User has current OneTimePassword but it is expired\
            **effects** deletes User's OneTimePassword\

**Note**: This concept will enhance security because not only would someone need to know your username and password, but also would need to have access to your email as well. Although better, this still leaves attacks where someone figures out how to find your account and email passwords (having to crack two passwords is much more difficult though).
