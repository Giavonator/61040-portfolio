# Assignment 1
## 1. Excercise 1
 1. **Invariants**. *What are two invariants of the state?*
 a)  Count for an Item within a Request must be nonnegative.
 b)  All Purchases must be associated with a Request.
 c)  In my opinion the second invariant is more important as the whole point of the GiftRegistration concept is to buy gifts that the owner User wants. If there are purchases that don't fall under Requests then those are gifts the owner didn't want. The purchase action is most affected by it as it must keep track that Purchases are buying for pre registered Items, and it does this by the *"requires Registry exists..."* clause.
.
 2. **Fixing an action**. *Can you identify an action that breaks this important invariant?*
  a) removeItem currently could break the invariant as it will *"remove the request from the Registry"*, irregardless if a Purchase has already been made for that item.
  b) This problem could be fixed by adding to the removeItem action's requirement to verify that the item does not already have associated Purchases for it.
.
 3. **Inferring behavior**. *By reading the specs of the concept actions, should a Registry be allowed to open and close repeatedly?*
 a) The open/close actions only require that the Registry is active/inactive respectively, therefore allowing to open and close the Registry several times.
 b) A reason to allow this is if owner Users may want to close the Registry temporarily while they are adding more Requests, and then reopen it whenever they are done.
.
 4. **Registry deletion**. *There is no action to delete a Registry. Would this matter in practice?*
 a) It could matter if an owner User doesn't want the Registry anymore, irregardless if it is open/closed.
 b) Potential storage implications for Registrys that can pile up and never be deleted.
.
 5. **Queries**. *What are two common queries likely to be executed against the concept state?*
 a) Registry owner query: List of gifts already purchased.
 b) Giver of a gift query: List of remaining possible gifts and their associated counts.
.
 6. **Hiding purchases**. *How would you augment the concept specification to support Registry owner surprises?*
 a) Modify state to include "a surprise Flag" for each one of the Registrys.
 b) Add to set of Purchases that they're only visible to owner if "surprise Flag" is false.
 .
 7. **Generic types**. *The User and Item types are specified as generic parameters. Why is this preferable?*
 a) Because defining *things* is complicated! I could want a boat, a dog, a house, or any random list of things in my Registry.
 b) It is better to reduce complexity of the GiftRegistration concept by having a different Item concept and passing it in.

## 2. Excercise 2

**concept** PasswordAuthentication
**purpose** limit access to known users
**principle** after a user registers with a username and a password,
they can authenticate with that same username and password
and be treated each time as the same user
**state**
    a set of Users with
        a confirmed Flag
        a token String
        a username String
        a password String
        an email String
  **actions**
    register (username: String, password: String, email: String): (user: User, token: String)
         **requires** no User exists with username
         **effects** creates new User with confirmed set to false, synchronized w/ other concept to email token to User
    authenticate (username: String, password: String): (user: User)
         **requires** User exists with that username and password, AND their confirmed Flag is set to true
         **effects** they are authenticated as the returned User and able to view other concepts data as that User
    confirm (username: String, token: String)
         **requires** User exists with that username and their confirmed Flag is false
         **effects** User's confirmed Flag set to true

3. *What essential invariant must hold on the state? How is it preserved?*
  To me, the most important invariant is that there should be NO duplicate username in the set of users. This is preserved within the register action, as it verifies no User already exists with that username before registering the new User.

## 3. Excercise 3

**concept** PersonalAccessToken [Scope]
**purpose** grant non-modifying access to registered user accounts
**principle** after a user registers with a username and a password,
they can create a personal access token that allows others to access a subset
of their account scopes without modifying what the user can actually access
**state**
    a set of Users with
        a username String
        a password String
        a set of Tokens
        a set of Scopes
    a set of Tokens with
        a name String
        an expiration Date
        a set of Scopes // token signins only can view scopes defined in their token
  **actions**
    register (username: String, password: String): (user: User)
         **requires** no User exists with username
         **effects** creates new User
    authenticate (username: String, password: String): (user: User)
         **requires** User exists with that username and password, OR valid token exists within that username with that token password
         **effects** they are authenticated as the User and only capable of accessing resources defined in their set of Scopes
    generateToken (username: String, password: String, name: String, expiration: Date, scopes: Scopes)
         **requires** User exists with that username and password (ie User owner not Token), AND no token exists in that username with 'name'
         **effects** new Token added to set of Tokens for User

**Note**: The PersonalAccessToken concept differs from PasswordAuthentication in one main factor, it allows people to grant other people access to a subset of their Scopes. Best explained via example (little long, optional example):
    **Ex**: Organization MIT has three departments: CS, Math, and Humanities who have a shared group of necessary resources, but each also have department specific resources. With PersonalAccessToken concept we can have one MIT User that creates three distinct personal access tokens that define the necessary scopes for each department (easy, central, and configurable in one account by MIT). On the other hand with PasswordAuthentication we would need 4 different accounts (MIT, MIT-CS, MIT-Math, MIT-Humanities) and configure everything from each one of those accounts. Very similar concepts, but very different end user experience.

**Change GitHub Documentation**: The best way to avoid confusion would to have an explicit section explaining (with an example like above) the differences between the two concepts, as they are so similar. That way they are able to accomidate more of the wide variety of user experiences/knowledge.










