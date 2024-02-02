# World-Cup-2023
Players Performance in world cup 2023
show databases;
use cricket_2023;
##Bowling Summary:

##1. Retrieve all bowling records.
SELECT * 
FROM `bowling summary`;

##2. Get the total number of wickets taken by each bowler.
SELECT Bowler_Name, SUM(Wickets) AS Total_Wickets
FROM `bowling summary`
GROUP BY Bowler_Name;

##3. Find the average economy rate for each bowling team.
SELECT Bowling_Team, AVG(Economy) AS Avg_Economy
FROM `bowling summary`
GROUP BY Bowling_Team;

##4. Identify the matches where a bowler took more than 3 wickets.
SELECT Match_no, Bowler_Name, Wickets
FROM `bowling summary`
WHERE Wickets > 3;

##5. Retrieve the top 5 bowlers with the best economy rates.
SELECT Bowler_Name, Economy
FROM `bowling summary`
ORDER BY Economy
LIMIT 5;

##6. Find the matches where a bowler bowled a maiden over.
SELECT Match_no, Bowler_Name, Overs, Maidens
FROM `bowling summary`
WHERE Maidens > 0;

##7. Calculate the average runs conceded per over for each bowler.
SELECT Bowler_Name, AVG(Runs/Overs) AS Avg_Runs_Per_Over
FROM `bowling summary`
GROUP BY Bowler_Name;

##8. Identify the bowler with the best bowling performance (maximum wickets) in each match.
SELECT Match_no, Bowler_Name, MAX(Wickets) AS Best_Bowling_Performance
FROM `bowling summary`
WHERE Wickets > 2
GROUP BY Match_no, Bowler_Name;

##9. Find the matches where a bowler had an economy rate below 4.
SELECT Match_no, Bowler_Name, Economy
FROM `bowling summary`
WHERE Economy < 4;

##10. Retrieve the bowlers who have bowled the most number of overs in the tournament.
SELECT Bowler_Name, SUM(Overs) AS Total_Overs
FROM `bowling summary`
GROUP BY Bowler_Name
ORDER BY Total_Overs DESC;

##11. Selecting columns and calculating aggregates for each bowler in a specific match
SELECT 
    `bowling summary`.Match_no,
    `bowling summary`.Bowling_Team,
    `bowling summary`.Bowler_Name,
    SUM(`bowling summary`.Overs) AS Total_Overs_By_Bowler,
    SUM(`bowling summary`.Wickets) AS Total_Wickets_In_Match
FROM 
    `bowling summary`
WHERE 
    `bowling summary`.Match_no = 2
GROUP BY 
    `bowling summary`.Match_no, `bowling summary`.Bowling_Team, `bowling summary`.Bowler_Name;

##Batting Summary:

##12. Retrieve all batting records.
SELECT * FROM `batting summary`;

##13. Get the total runs scored by each batsman.
SELECT Batsman_Name, SUM(Runs) AS Total_Runs
FROM `batting summary`
GROUP BY Batsman_Name
ORDER BY Total_Runs DESC; 

##14. Find the average strike rate for each batting position.
SELECT Batting_Position, AVG(Strike_Rate) AS Avg_Strike_Rate
FROM `batting summary`
GROUP BY Batting_Position;

##15. Identify the matches where a batsman scored a century (100 runs or more).
SELECT Match_no, Batsman_Name, Runs
FROM `batting summary`
WHERE Runs >= 100
ORDER BY Runs DESC;

##16. Retrieve the top 5 batsmen with the highest strike rates.
SELECT Batsman_Name, Strike_Rate
FROM `batting summary`
ORDER BY Strike_Rate DESC
LIMIT 5;

##17. Identify the batsmen who faced the most number of balls in a single match.
SELECT Match_no, Batsman_Name, Balls
FROM `batting summary`
ORDER BY Balls DESC
LIMIT 10;

##18. Calculate the average runs scored per match for each batsman.
SELECT Batsman_Name, AVG(Runs) AS Avg_Runs_Per_Match
FROM `batting summary`
GROUP BY Batsman_Name;

##19. Find the matches where a batsman hit more than 3 sixes.
SELECT Match_no, Batsman_Name, 6s
FROM `batting summary`
WHERE 6s > 3;

##20. Retrieve the batsmen who scored the most number of boundaries (4s + 6s) in a single match.
SELECT Match_no, Batsman_Name, 4s, 6s, (4s + 6s) AS Total_Boundaries
FROM `batting summary`
ORDER BY Total_Boundaries DESC
LIMIT 10;

##21. Get the batting average for each batting position.
SELECT Batting_Position, AVG(Runs) AS Batting_Average
FROM `batting summary`
GROUP BY Batting_Position;

##22. Find the batsmen who were not dismissed (DNB - Did Not Bat) in a match.
SELECT Match_no, Batsman_Name, Dismissal
FROM `batting summary`
WHERE Dismissal = 'DNB';

##23. Identify the matches where a batsman scored between 50 and 100 runs.
SELECT Match_no, Batsman_Name, Runs
FROM `batting summary`
WHERE Runs BETWEEN 50 AND 100;

##24. Calculate the total number of runs scored by each team across all matches.
SELECT Team_Innings, SUM(Runs) AS Total_Runs
FROM `batting summary`
GROUP BY Team_Innings;

##25. Retrieve the batsmen who maintained a strike rate above 150 in a match.
SELECT Match_no, Batsman_Name, Strike_Rate
FROM `batting summary`
WHERE Strike_Rate > 150;

##26. Get the top 5 batsmen with the highest average runs per match.
SELECT Batsman_Name, AVG(Runs) AS Avg_Runs_Per_Match
FROM `batting summary`
GROUP BY Batsman_Name
ORDER BY Avg_Runs_Per_Match DESC
LIMIT 5;


##27. Left Join - All Bowling Records and Matching Batting Records:
SELECT `bowling summary`.*, `batting summary`.*
FROM `bowling summary`
LEFT JOIN `batting summary`ON `bowling summary`.Match_no = `batting summary`.Match_no;

##28. Right Join - Retrieve All Batting Records and Matching Bowling Records:
SELECT `bowling summary`.*, `batting summary`.*
FROM `bowling summary`
RIGHT JOIN `batting summary` ON `bowling summary`.Match_no = `batting summary`.Match_no;

##29. Join with Conditions - Retrieve Matches Where Bowler Took Wickets and Batsman Scored Runs:
SELECT `bowling summary`.Match_no, `bowling summary`.Bowling_Team, `bowling summary`.Bowler_Name, `batting summary`.Runs, `bowling summary`.Wickets
FROM `bowling summary`
INNER JOIN `batting summary` ON `bowling summary`.Match_no = `batting summary`.Match_no
WHERE `bowling summary`.Wickets > 1 AND `batting summary`.Runs < 5;

