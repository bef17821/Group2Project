# MIST 4610 Group 2 Project 1

## Team Members 
1. Brooke Francis
2. Sophia Tran
3. Pranav Saravanakumar
4. Brandon Sevel
5. Hita Boddu

## Problem Description:

The task at hand is to model and build a reltional database for the general workings of a collegiate athletics program focused on its team roster and operations. The centeral entity in the model is the Players entity because it is the individual athletes whose information connects practices, positions, academics, equipment, injuries, awards, statistics, and NIL activity.

## Data Model Description: 

<img width="1782" height="1024" alt="image" src="https://github.com/user-attachments/assets/61e60e18-b439-4af2-a773-7371879c7275" />

Our model is based on the structure of an athletics roster database. The Players entity stores each athlete (with attributes such as playerName and physical measures), and it is the hub for the rest of the system. Players has a many-to-one relationship with primaryPosition, where a position records data like positionID, positionType, and the number of players at that position. Players reference their primaryPosition, so each position can have many players assigned to it.

There is a role relationship in the position area as well. primaryPosition includes captainID and captainName, and it connects to players through a labeled “Captain” relationship to indicate that a position designates a specific player as captain. Inside Players there is also a recursive “Mentor” relationship through mentorID, showing that one player can serve as a mentor for other players.

Academic information is modeled by the academic_record table. Each players record can have an associated academic_record capturing items such as GPA, creditHours, expectedGraduationDate, and probationStatus. This produces a one-to-many relationship from Players to Academic_Record so that academic snapshots can be stored per player as needed.

Player performance is captured in two places tied back to players. First, the stats table stores seasonal performance metrics (playerRating, season, gamesPlayed, snapsPlayed) and relates to players in a one-to-many fashion so multiple stat lines can exist per athlete. Second, practice participation is handled through an associative entity. Because a player can attend many practices and each practice contains many players, we created practice_attendance between practice and players. Practice holds the practiceType, practiceDate, practiceLocation, and practiceDuration, while practice_attendance tracks items such as performanceGrade, timeSpent, fullParticipant, and playsCompleted.

Health data is split between a catalog of injuries and a player-specific history. Injury lists injury types and attributes such as injurySeverity, injuryTreatmentLocation, and bodyPart. injury_history is the associative entity between players and injury and adds event details like InjuryDate, InjuryTime, and expectedRecoveryTime. This allows the database to represent many injuries per player and many players experiencing the same injury type.

Equipment issued to players in the equipment table. Each record includes equipmentType, equipmentSize, equipmentCondition, lastInspectionDate, purchaseDate, and warrantyExpirationDate and is linked to players, giving a one-to-many relationship from players to equipment so that multiple pieces of equipment can be managed per athlete.

Awards granted to players are modeled with a standard many-to-many pattern. Award stores award attributes such as awardName, awardSponsor, and trophyType. Because a player can receive many awards and an award can be conferred to many players over time, we created the conferment associative entity between award and players. Conferment records details like ConfermentDate and provides a unique ConfermentID to identify each award event.

Finally, NIL activity is represented by two tables that connect sponsors and players. NIL_sponsor contains sponsor information (sponsorName, fundNetWorth, address, city, state, industry). NIL_contract serves as the associative entity between players and nil_sponsor, capturing contractName, contractSponsor, contractType, contractValue, contractDuration, contractAwardedDate, and contractEndDate. This structure supports many contracts per player and many contracts per sponsor, with each contract clearly tied to both a specific player and a specific sponsor.

Overall, the players entity anchors the database. From it branch many-to-one relationships to primary position, academics, statistics, equipment, and injury history; many-to-many relationships are resolved through associative entities for practice attendance, award conferment, and NIL contracts; and recursive relationships handle mentors and position captains. This design cleanly captures the roster, activities, and records shown in the data model.


## Data Dictionary:
<img width="994" height="720" alt="image" src="https://github.com/user-attachments/assets/12f74a72-7b52-4d4f-8986-8ed386befd6e" />
<img width="970" height="632" alt="image" src="https://github.com/user-attachments/assets/3035bed0-5608-4b93-8f5b-4ddd6f3e07be" />
<img width="972" height="410" alt="image" src="https://github.com/user-attachments/assets/5013e9ba-2a07-4ea0-9fb0-4754bb9baf07" />
<img width="974" height="900" alt="image" src="https://github.com/user-attachments/assets/8e4c3eb7-667f-42af-a9c1-c56898ccc431" />
<img width="982" height="402" alt="image" src="https://github.com/user-attachments/assets/da54b1b8-5498-493c-8a17-cb76c7ab355e" />
<img width="984" height="672" alt="image" src="https://github.com/user-attachments/assets/697231cb-1380-4b40-ab48-769bc2e81749" />
<img width="972" height="884" alt="image" src="https://github.com/user-attachments/assets/1366db3f-984e-456f-a79c-04c8fcc0dfc2" />
<img width="978" height="764" alt="image" src="https://github.com/user-attachments/assets/9e30e9c3-a7cd-4377-a9a5-287a590cd4af" />
<img width="976" height="788" alt="image" src="https://github.com/user-attachments/assets/ad4c8578-6083-4b20-8b31-84f84091ca24" />
<img width="970" height="516" alt="image" src="https://github.com/user-attachments/assets/9a6fd9c9-addc-4b2a-bb4a-e80151837295" />
<img width="968" height="692" alt="image" src="https://github.com/user-attachments/assets/77420402-e3b1-4416-8ae3-e71355c6dbd2" />
<img width="960" height="718" alt="image" src="https://github.com/user-attachments/assets/681c5b02-2ed3-46ce-82e6-b2c53ad586df" />
<img width="976" height="696" alt="image" src="https://github.com/user-attachments/assets/4410b237-57ce-4502-9b6a-793c8b6786b0" />

## Queries:

<img width="886" height="510" alt="image" src="https://github.com/user-attachments/assets/2f03fe44-5bbb-440c-8dad-1522d17fef1d" />


### Query 1 
This query lists players whose GPA is less than 2.5 and who have logged more than 100 snaps this season.

<img width="650" height="450" alt="image" src="https://github.com/user-attachments/assets/761b12d7-2c69-4692-919b-b1127fdf327c" />

### Result:

<img width="300" height="500" alt="image" src="https://github.com/user-attachments/assets/a6e9d2d4-cdaf-43be-93e0-6f42336fdc45" />

This query helps staff identify which players are at risk academically with heavy athletic workloads. It supports academic support and coaching staff in targeting interventions for athletes that are really involved in games but also at risk of losing academic eligibility. Identifying these players is important in allocating academic resources and reducing playing time to support academic and athletic success.

### Query 2 
This query lists each player's name, the date of their latest injury, and the injury severity

<img width="1050" height="260" alt="image" src="https://github.com/user-attachments/assets/a047974c-82ad-4fac-97bc-a0ddf7cda212" />

### Result: 

<img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/4d57034b-e4cd-4746-a166-63bf93538652" />

This query gives medical and coaching staff a way to see each player's most recent injury. Looking at the date and severity of past injuries is important, especially for athletes as it helps monitor recovery progress and allocate training workload. With this information, staff can plan the roster and make training adjustments based on each player's most recent injury.

### Query 3 
This query shows the number of NIL contracts and total value by sponsor industry in descending order

<img width="1230" height="136" alt="image" src="https://github.com/user-attachments/assets/f16ab17c-746a-444a-8e8e-15df4cc2d626" />

### Result: 

<img width="400" height="174" alt="image" src="https://github.com/user-attachments/assets/5533855f-656f-4690-9b88-5273ba3ff0fd" />

This query helps administrators understand which industries are most invested in the program and they can use that data to assess financial dependency or outreach gaps. Understanding which industries bring in the most money and contracts can help staff position their players towards those industries.

### Query 4 
This Query lists each mentor, their average player rating, and the average rating of their mentors. It includes only players that mentor at least one mentee.

<img width="1232" height="176" alt="image" src="https://github.com/user-attachments/assets/ffa02135-088e-43a8-bece-03dcf868a58d" />

### Result: 

<img width="500" height="250" alt="image" src="https://github.com/user-attachments/assets/72132cf1-0322-4ed7-85ea-ff81f4e32005" />

This query shows how each mentor's performance relates to their mentees' average performance over time. This will help show a strong correlation between mentors performance and their mentee's performance, which helps staff see which mentors exhibit strong leadership and growth within the team. 

### Query 5 
This query lists each player, the total number of minutes they spent in practice, and their average player rating.

<img width="800" height="300" alt="image" src="https://github.com/user-attachments/assets/6e68366f-ec25-4d5f-96ad-8218cc97073e" />

### Result:

<img width="500" height="700" alt="image" src="https://github.com/user-attachments/assets/5fa6c891-25cc-44a0-b76e-e93c33373250" />

This query shows you whether players who practice more tend to have higher performance ratings and it helps coaches and performance staff analyze correlations between practice and training effort and performance on the field. If there is a positive correlation seen there, managers and staff could incentive players to practice more and put more effort into training for increased performance rating.  

### Query 6 
This query lists of players who are academically eligible, meaning their GPA is greater than 2.0 or they are not currently on academic probation. It joins the players table with the academic_record table to show each player’s name, GPA, and probation status.

<img width="600" height="150" alt="image" src="https://github.com/user-attachments/assets/ecee9280-a28e-4d60-aa3a-42260cb6183c" />

### Result:

<img width="400" height="700" alt="image" src="https://github.com/user-attachments/assets/e954567d-49be-4464-afdf-d72cd7640f32" />

From a management standpoint, this query quickly identifies which players are in good academic standing and therefore eligible to participate in team activities or competitions. Coaches and academic advisors can use this information to ensure compliance with eligibility rules, plan playing rosters, and focus support efforts on players who may be at academic risk.

### Query 7 
This query lists all players who have received an award. It joins the players, conferment, and award tables to display each player’s name along with the award name, trophy type, and sponsor. The DISTINCT keyword ensures each player-award combination is listed only once.

<img width="800" height="260" alt="image" src="https://github.com/user-attachments/assets/847dd103-9978-428b-9ed6-7a5ad35f8a01" />

### Result:

<img width="600" height="164" alt="image" src="https://github.com/user-attachments/assets/9113af00-caa4-43c2-a640-351a3861001e" />

This query helps management and communications staff easily identify and recognize player achievements. It supports tasks such as updating team websites, social media, or reports highlighting standout athletes, and it can also be used for award ceremonies or alumni engagement efforts.

### Query 8 
This query calculates the average GPA for players in each position group. It converts position abbreviations (like MLB or QB) into their full names using a CASE statement. It then compares each position’s average GPA to the team’s overall GPA, showing only the positions that fall below the team average. The results are listed in ascending order of average GPA.

<img width="600" height="700" alt="image" src="https://github.com/user-attachments/assets/eda731d0-54cb-460d-90f1-3beb362aec4a" />

### Result:

<img width="300" height="200" alt="image" src="https://github.com/user-attachments/assets/1b37a74a-4a08-42ac-995e-567ccef5a538" />

This query helps coaches and academic advisors identify position groups that may be underperforming academically. Managers can use this information to target academic support, tutoring, or schedule adjustments for specific groups of players, ensuring that academic performance is consistent across the team.


### Query 9 
This query lists players whose average practice performance grade is higher than the overall team average. It joins the players table with the practice_attendence table, calculates each player’s average performance grade and total plays completed, and then filters the results to show only above-average performers.

<img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/d889c96b-8112-49d4-80f2-7c560d36ccdf" />

### Result:

<img width="400" height="600" alt="image" src="https://github.com/user-attachments/assets/fb06ac55-ab3f-46b2-929b-2e609ff40f03" />

This query helps coaches and training staff identify the most consistent and productive players during practice sessions. Recognizing top performers can guide decisions about starting lineups, leadership roles, or specialized training programs. It also provides data-driven insight into which players are exceeding expectations and contributing the most in practice.

### Query 10 
This query calculates the average practice performance for each position group and compares it to the overall team average. It joins the players, primaryPosition, and practice_attendence tables to group performance data by position and shows only the positions performing above the team-wide average.

<img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/3984a7bc-60be-4b98-9d7f-706f0e341b1e" />

### Result:

<img width="300" height="100" alt="image" src="https://github.com/user-attachments/assets/42766217-e6be-47f4-a65e-355dfd6a79a4" />

This query allows coaches and team managers to evaluate which position groups are performing best during practices. By highlighting strong-performing units, managers can recognize effective training strategies, reward consistent groups, and identify which areas may need additional coaching or attention to improve overall team balance.



## Database Information: 
Name of the database: ns_Group2

- Each query is a stored procedure in the database and can be called using the format TP_Q1();
