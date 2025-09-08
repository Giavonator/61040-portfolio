# Assignment 1
## 1. Domains
### 1.1 Brainstorm Domains
- *MIT Solar Electric Vehicle Team*: Building a solar vehicle with friends.
- *MIT Men's Soccer Club*: Kick a ball around, but competitively!
- *La Maison Française*: My cultural house within New House.
- *Competitive Programming*: LeetCode, but competitively (CodeForces)!
- *Cooking/Eating*: Who doesn't love food!
- *Family*: Won't see them for several months, but miss them lots!
- *Classes/Schedule*: Keeping your calendar/timeline in check is important!
- *Sleep*: Speaking of which, maybe I need a nap.
- *Working out*: Personally, I do a MWF PPL split.
- *Meditation*: Although not a proffesional, something I've been trying recently.

### 1.2 Most Promising Domains
- La Maison Française (LMF): Located on the West half of New House 4th floor, around 30 students live together with a shared love for France. This is where I've called home for all of my undergrad and where my deepest friendships have been created over the semesters. In my heart considered as my home away from home.
- MIT Solar Electrive Vehicle Team: I spend around 10 hours every work dedicated to the design and development of our solar car Solstice. The 25-26 school year we must get done a lot of the manifacturing, and hopefully should be all ready to compete next summer!
- MIT Men's Soccer Club: If there was one thing I've loved for longer than software, it 100% would be soccer. Being Uruguayan we don't grow up with religion, but rather praying to our favorite national team players to beat our rivals Argentina and Brazil.

## 2. Problems

### 2.1 Brainstorm Problems

#### 2.1.1 MIT Men's Football Club (MFC):

1. Attendance + Stats: Practice/game attendance is tracked through clunky spreadsheet and no history is maintained, along with almost no game/practice stat tracking.

2. Performance: Playing time is directly related to our performance, but with the coach being our captain biases come through and playing time is affected.

3. Tardiness: Players are constantly late, with no reprocussions. Along with no record of tardiness.

#### 2.1.2 La Maison Française (LMF):

1. Requesting Subs: Our house is built around a cooking system, but the current process for asking for a cooking sub is not great.

2. Food Management: We need to feed 30+ people every day for dinner, therefore, food management is such an issue that we have two people dedicated to managing it.

3. Nettoyage Points: We have a chore system at our house, but managed through slack makes it clunky and lacks transparency.


#### 2.1.3 MIT Solar Electric Vehicle Team (SEVT):

1. Organization: Currently no system is in place tracking who is working on what.

2. Attendance: Schedules are erradict, not ever really sure who will be in lab or when.

3. Lack of social outings: All of last year there were only 1-2 social outings, a number that could be improved with organized event planning software.


### 2.2 Great Filtering


#### 2.2.1 Rejected

1. *SEVT Social Outings*:
    - Indifference: If people cared enough there would have been more outings.
    - Lack of Critical Mass: Not many people attended the outings, therefore I don't believe many people would use this solution for it.

2. *SEVT Attendance*:
    - Friction: If hectic MIT schedules prevent members to show up consistently at same times, where would they get the extra time for this?
    - Insufficient Differentiation: Difficult to make something that spreadsheets can't already do.

3. *LMF Nettoyage Points*:
    - Antibodies: Keeping track of chores generally has lots of problems associated, like someone seing they are at the bottom of chore completion percentage.
    - Insufficient Differentiation: Difficult to make something that spreadsheets can't already do.

4. *SEVT Organization*:
    - Friction: Hectic schedules prevent spreadsheets to be maintained, how what that be any different here?
    - Insufficient Differentiation: Difficult to make something that spreadsheets can't already do.

5. *MFC Performance*:
    - Antibodies: Sub par performing players will react negatively seeing themselves on the bottom of the team.
    - Unexpected Consequences: Introducing this could cause a lot of tension and problems within the team in regards to how performance is calculated, or "Why is XXX above XXX when XXX?" ect.

6. *MFC Tardiness*:
    - Unexpected Consequences: What if people that would've showed up late just don't show up anymore in order to avoid being late?
    - Indifference: Is people showing up late really that big of a problem?

#### 2.2.1 Problems Moving On

After filtering six of the problems, the three major problems moving on willl be *LMF Food Management*, *LMF Sub Request System*, and *MFC Attendance + Stats*.

For a details into why they were selected, stakeholder analysis, evidence/comparable consideration, and feature consideration, please visit move onto the next section.

## 3. Potential Projects

### 3.1 LMF Food Management
#### 3.1.1 Selection Explanation
The biggest reason as to why this problem moved forward, was due to its authentic demand. Currently we have two house members spending around 5-7 hours a week managing all of the food for the house, a crazy 10-14 hours a week that could be used otherwise! Although there are some considerations like how to keep track of food expiration, how to add massive amounts of weekly incoming food, and how to integrate it into a system of 30+ people, but ultimately if I were to succeed with this project it would 100% be a "NOT NOT" usable thing for our house.

#### 3.1.2 Key Stakeholder
  1.  Cook Team Members (Students apart of the house, cooking roles): These house members are a part of a cookteam, and every 5-6 weeks they need to plan a menu. Their direct affect would be the user experience difference between writing menus in Microsoft Word or my LMF Food Management system.
  2.  Food Stewards (Students apart of the house, that manage food): These would be the most impacted house members, as depending on the project features could automate a great deal of their weekly tasks. Key impacts for them would be: automatic centralization of weekly ingredient purchase list across all menus, automatic taking care of food expiration, and more depending on features.
  3.  Treasurer (Student apart of the house, that manage finances): Historical cost week over week for menus can be easily stored and provided simply for finances. Simplifying them to no longer need to keep track of and add up all the receipts.

#### 3.1.3 Evidence/Comparables

#### 3.1.4 Potential Features
##### 3.1.4.1 Sigma Ingredients
Adding up all of the ingredients accross all menus for the week is very time consuming, but this feature would automatically due so when menus are input into the system. On top of this, ingredients are grouped into what grocery store we would purchase from them.

##### 3.1.4.2 Expiration, Oh No!
For the weekly food purchases, sometimes we know that a certain food will not be used. This feature will automatically keep track of that and inform the food stewards whenever something was expiring soon.

##### 3.1.4.3 Order on Demand
Not sure exactly how possible this would be, but this feature would automatic load the menu ingredients into online shopping orders. Allowing food stewards to simply look over them and hit purchase! Nice and easy!





### 3.2 LMF Sub Request System
#### 3.2.1 Selection Explanation
Personally, one of my biggest pet peeves is constantly receiving emails when they either don't apply to me or I don't care about its contents. Our current LMF Sub Request System is simply email **THE WHOLE HOUSE** asking for a sub, and constantly bumping with additional emails if no one responds. This becomes a slight burden within the house when trying to be considerate and subbing when you can, as you can spend close to 30 minutes a week figuring this out. Ultimately another "NOT NOT" usable solution if implemented correctly.


#### 3.2.2 Key Stakeholders
Stakeholder roles change on an email by email bases regarding whether you would be able to sub for someone. This is because you are only able to sub a portion of the sub requests that get sent to the house.

  1.  Not capable of subbing members (Can't sub current emailed sub request): Direct impact would be no longer receiving the email at all. System would take into account your availability and only notify you if you are free.
  2.  Capable of subbing members (Can sub current emailed sub request): Now whenever you get an email, you know that you *should* be able to sub. Potentially a group chat or group emaling thread could be open across everyone that would be free, that way we can increase communication for subs.
  3.  Never capable of subbing (GRAs, Food Stewards, Certain roles): Some house memebrs unfortunately get added to all sub requests, even though they aren't supposed to ever sub. This project would then prevent them from being annoyingly emailed ever again.

#### 3.2.3 Evidence/Comparables

#### 3.2.4 Potential Features
##### 3.2.4.1 Sub Pls?
This feature would automatically map a sub to house member availabilities, and determine who could potential do the sub. Then automatically communicate to those particular individuals.

##### 3.2.4.2 Email+
Instead of having to email everyone, this feature would integrate some sort of instant messaging system to increase response efficiency. Whether this is creating a slack channel, message group chat, ect., simply some sort of communication platform better than email.

##### 3.2.4.3 Composite Subbing
What happens if not a single person could sub for the entire three hours? Then maybe grouping of people could take different portions of the sub? This feature would kick in if everyone said no for full subs, and send further sub requests in pairs.




### 3.3 MFC Attendance + Stats
#### 3.3.1 Selection Explanation
As someone who regularly attends practices, but doesn't get too much playing time, it sometimes can be frustrating when your attendance isn't being accounted for. On top of this, due to our sub par attendance tracking system, our practices/games consistently have an unreliable number of players. This combines to difficulty in planning practices/games and them being unreliable metrics for individual playing time.

#### 3.3.2 Key Stakeholders

  1.  Captain (Essentially Coach/Player role): The impact of the problem is that the captain has very limited data with attendance and stats to determine who plays the next game.
  2.  Regular Player: The biggest problem as a player who is consistently there that doesn't get playing time is that as players we don't know what is being considered when deciding playing time. By bringing in hard numbers a general sense of transparence would be brought to the team.
  3.  Outside Viewer (Non team member): People outside the team have zero way of knowing who is attending or how they are doing.

#### 3.3.3 Evidence/Comparables

#### 3.3.4 Potential Features
##### 3.3.4.1 Team History
A year long aggregation of player attendance based on practices and games. This feature would be filterable by specific date, date range, player, or grouping of players. Allows for easy trend analysis to be done on whether a player is increasing attendance or decreasing.

##### 3.3.4.2 Futurama
In order for a game to be rescheduled the team needs to notify the league at least a week before, so this feature would ensure that we are able to meet that deadline. Containing practice/game dates as far into the future as we know, allows for players to mark their availability and keep track of it in anticipation of deadlines.

##### 3.3.4.3 Stat Tracker
Automatic survey sent to players after every game to gather data on player scoring, assissts, and overall stats of the players.








