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

<img width="500" height="500" alt="image" src="https://github.com/bef17821/Group2Project/blob/main/IMG_7381.PNG" />

Explanation of Data Model: 

Our model is based on the structure of an athletics roster database. The Players entity stores each athlete (with attributes such as playerName and physical measures), and it is the hub for the rest of the system. Players has a many-to-one relationship with Primary_Position, where a position records metadata like positionID, positionType, and the number of players at that position. Players reference their Primary_Position, so each position can have many players assigned to it.

There is a role relationship in the position area as well. Primary_Position includes captainID and captainName, and it connects to Players through a labeled “Position Captain” relationship to indicate that a position designates a specific player as captain. Inside Players there is also a self-referential “Mentor” relationship through mentorID, showing that one player can serve as a mentor for other players.
Academic information is modeled by the Academic_Record table. Each Players record can have an associated Academic_Record capturing items such as GPA, creditHours, expectedGraduationDate, and probationStatus. This produces a one-to-many relationship from Players to Academic_Record so that academic snapshots can be stored per player as needed.

Player performance is captured in two places tied back to Players. First, the Stats table stores seasonal performance metrics (playerRating, season, gamesPlayed, snapsPlayed) and relates to Players in a one-to-many fashion so multiple stat lines can exist per athlete. Second, practice participation is handled through an associative entity. Because a player can attend many practices and each practice contains many players, we created Practice_Attendance between Practice and Players. Practice holds the practiceType, practiceDate, practiceLocation, and practiceDuration, while Practice_Attendance tracks items such as performanceGrade, timeSpent, fullParticipant, and playsCompleted.

Health data is split between a catalog of injuries and a player-specific history. Injury lists injury types and attributes such as injurySeverity, injuryTreatmentLocation, and bodyPart. Injury_History is the associative entity between Players and Injury and adds event details like InjuryDate, InjuryTime, and expectedRecoveryTime. This allows the database to represent many injuries per player and many players experiencing the same injury type.

Equipment issued to players is captured by Equipment_Set. Each record includes equipmentType, equipmentSize, equipmentCondition, lastInspectionDate, purchaseDate, and warrantyExpirationDate and is linked to Players, giving a one-to-many relationship from Players to Equipment_Set so that multiple pieces of equipment can be managed per athlete.

Awards granted to players are modeled with a standard many-to-many pattern. Award stores award attributes such as awardName, awardSponsor, and trophyType. Because a player can receive many awards and an award can be conferred to many players over time, we created the Conferment associative entity between Award and Players. Conferment records details like ConfermentDate and provides a unique ConfermentID to identify each award event.

Finally, NIL activity is represented by two tables that connect sponsors and players. NIL_Sponsor contains sponsor information (sponsorName, fundEndowment, address, city, state, industry). NIL_Contract serves as the associative entity between Players and NIL_Sponsor, capturing contractName, contractSponsor, contractType, contractValue, contractDuration, contractAwardedDate, and contractEndDate. This structure supports many contracts per player and many contracts per sponsor, with each contract clearly tied to both a specific player and a specific sponsor.

Overall, the Players entity anchors the database. From it branch many-to-one relationships to primary position, academics, statistics, equipment, and injury history; many-to-many relationships are resolved through associative entities for practice attendance, award conferment, and NIL contracts; and special role relationships handle mentors and position captains. This design cleanly captures the roster, activities, and records shown in the data model.


## Data Dictionary:

## Queries:
1. Query 1 lists players whose GPA is less than 2.5 and who have logged more than 100 snaps this season.
<img width="500" height="100" alt="image" src="https://github.com/user-attachments/assets/761b12d7-2c69-4692-919b-b1127fdf327c" />

Result:

<img width="200" height="300" alt="image" src="https://github.com/user-attachments/assets/a6e9d2d4-cdaf-43be-93e0-6f42336fdc45" />

This query helps staff identify which players are at risk academically with heavy athletic workloads. It supports academic support and coaching staff in targeting interventions for athletes that are really involved in games but also at risk of losing academic eligibility. Identifying these players is important in allocating academic resources and reducing playing time to support academic and athletic success.

2. Query 2 lists each player's name, the date of their latest injury, and the injury severity
<img width="850" height="160" alt="image" src="https://github.com/user-attachments/assets/a047974c-82ad-4fac-97bc-a0ddf7cda212" />

Result: 

This query gives medical and coaching staff a way to see each player's most recent injury. Looking at the date and severity of past injuries is important, especially for athletes as it helps monitor recovery progress and allocate training workload. With this information, staff can plan the roster and make training adjustments based on each player's most recent injury.

3. Query 3 shows the number of NIL contracts and total value by sponsor industry in descending order

This query helps administrators understand which industries are most invested in the program and they can use that data to assess financial dependency or outreach gaps. Understanding which industries bring in the most money and contracts can help staff position their players towards those industries.


4. Query 4 lists each mentor, their average player rating, and the average rating of their mentors. It includes only players that mentor at least one mentee

This query shows how each mentor's performance relates to their mentees' average performance over time. This will help show a strong correlation between mentors performance and their mentee's performance, which helps staff see which mentors exhibit strong leadership and growth within the team. 

5. Query 5 lists each player, the total number of minutes they spent in practice, and their average player rating. 

This query shows you whether players who practice more tend to have higher performance ratings and it helps coaches and performance staff analyze correlations between practice and training effort and performance on the field. If there is a positive correlation seen there, managers and staff could incentive players to practice more and put more effort into training for increased performance rating. 

6. What the query does:
This query retrieves a list of players who are academically eligible, meaning their GPA is greater than 2.0 or they are not currently on academic probation. It joins the players table with the academic_record table to show each player’s name, GPA, and probation status.
Why it’s important from a managerial perspective:
From a management standpoint, this query quickly identifies which players are in good academic standing and therefore eligible to participate in team activities or competitions. Coaches and academic advisors can use this information to ensure compliance with eligibility rules, plan playing rosters, and focus support efforts on players who may be at academic risk.

7. What the query does:
This query lists all players who have received an award. It joins the players, conferment, and award tables to display each player’s name along with the award name, trophy type, and sponsor. The DISTINCT keyword ensures each player-award combination is listed only once.
Why it’s important from a managerial perspective:
This query helps management and communications staff easily identify and recognize player achievements. It supports tasks such as updating team websites, social media, or reports highlighting standout athletes, and it can also be used for award ceremonies or alumni engagement efforts.

8. What the query does:
This query calculates the average GPA for players in each position group. It converts position abbreviations (like MLB or QB) into their full names using a CASE statement. It then compares each position’s average GPA to the team’s overall GPA, showing only the positions that fall below the team average. The results are listed in ascending order of average GPA.
Why it’s important from a managerial perspective:
This query helps coaches and academic advisors identify position groups that may be underperforming academically. Managers can use this information to target academic support, tutoring, or schedule adjustments for specific groups of players, ensuring that academic performance is consistent across the team.


9. What the query does:
This query lists players whose average practice performance grade is higher than the overall team average. It joins the players table with the practice_attendence table, calculates each player’s average performance grade and total plays completed, and then filters the results to show only above-average performers.
Why it’s important from a managerial perspective:
This query helps coaches and training staff identify the most consistent and productive players during practice sessions. Recognizing top performers can guide decisions about starting lineups, leadership roles, or specialized training programs. It also provides data-driven insight into which players are exceeding expectations and contributing the most in practice.

10. What the query does:
This query calculates the average practice performance for each position group and compares it to the overall team average. It joins the players, primaryPosition, and practice_attendence tables to group performance data by position and shows only the positions performing above the team-wide average.
Why it’s important from a managerial perspective:
This query allows coaches and team managers to evaluate which position groups are performing best during practices. By highlighting strong-performing units, managers can recognize effective training strategies, reward consistent groups, and identify which areas may need additional coaching or attention to improve overall team balance.



## Database Information: 
