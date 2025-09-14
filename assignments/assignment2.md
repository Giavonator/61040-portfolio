# Assignment 1
## 1. Excercise 1
 1. **Invariants**. *What are two invariants of the state?*
 a)  Count for an Item within a Request must be nonnegative.
 b)  All Purchases must be associated with a Request.
 c)  In my opinion the second invariant is more important as the whole point of the GiftRegistration concept is to buy gifts that the owner User wants. If there are purchases that don't fall under Requests then those are gifts the owner didn't want. The purchase action is most affected by it as it must keep track that Purchases are buying for pre registered Items, and it does this by the *"requires registry exists..."* clause.
.
 2. **Fixing an action**. *Can you identify an action that breaks this important invariant?*
  a) removeItem currently could break the invariant as it will *"remove the request from the registry"*, irregardless if an Purchase has already been made for that item.
  b) This problem could be fixed by adding to the removeItem action's requirement to verify that the item does not already have associated Purchases for it.
.
 3. **Inferring behavior**. *By reading the specs of the concept actions, should a registry be allowed to open and close repeatedly?*
 a) The open/close actions only require that the registry is active/inactive respectively, therefore allowing to open and close the registry several times.
 b) A reason to allow this is that owner Users may want to close the registry temporarily while they are adding more Requests, and then reopen it whenever they are done.
.
 4. **Registry deletion**. *There is no action to delete a registry. Would this matter in practice?*
 a) It could matter if an owner User doesn't want the registry anymore, irregardless if it is open/closed.
 b) Potential storage implications for registries that can pile up and never be deleted.
.
 5. **Queries**. *What are two common queries likely to be executed against the concept state?*
 a) Registry owner query: List of gifts already purchased.
 b) Giver of a gift query: List of remaining possible gifts and their associated counts.
.
 6. **Hiding purchases**. *How would you augment the concept specification to support Registry owner surprises?*
 a) Modify state to include "a surprise Flag" for each one of the Registrys.
 b) With this flag we can modify queries during implementation to verify Registrys aren't surprises for the owner.
 .
 7. **Generic types**. *The User and Item types are specified as generic parameters. Why this is preferable?*
 a) Because defining *things* is complicated! I could want a boat, a dog, a house, or any random list of things in my registry.
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
        a token String // via sync other concept emails token to User
        a username String
        a password String
  **actions**
    register (username: String, password: String): (user: User, token: String)
         **requires** no User exists with username
         **effects** creates new User with confirmed set to false
    authenticate (username: String, password: String): (user: User)
         **requires** User exists with that username and password
         **effects** User is authenticated to access data stored in other concepts
    confirm (username: String, token: String)
         **requires** User exists with that username and hasn't been confirmed yet
         **effects** User's confirmed flag set to true

3. *What essential invariant must hold on the state? How is it preserved?*
  To me, the most important invariant is that there should be NO duplicate username in the set of users. This is preserved within the register action, as it verifies no User already exists that username before registering the new User.









