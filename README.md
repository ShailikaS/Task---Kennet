# Task---Kennet

# Assignment 6.1
https://drive.google.com/file/d/1sRP2AXifN7r2Y7Z4fg_-n4ZPmZim6lIB/view?usp=sharing

#Write SQL or Mongo queries for following reports:

1. Player’s strike rate -> Total Runs divided by matched played.
 
  : SELECT player_name, total_runs / total_matches_played AS StrikeRate
   FROM Player;

2. Player’s avg run-rate -> Total Runs divided by overs played
 
  : SELECT player_name, total_runs / total_overs_played AS AvgRunRate
   FROM Player;


3. Player’s Top 3 matches according to strike rate.

  : SELECT p.player_name, m.match_id, (mp.runs_scored / (m.team_1runs + m.team_2runs)) AS StrikeRate
   FROM Player p
   JOIN MatchPlayerPerformance mp ON p.player_id = mp.player_id
   JOIN Match m ON mp.match_id = m.match_id
   ORDER BY StrikeRate DESC
   LIMIT 3;


4. Couple of teams who have played most matches with each-other.

   : SELECT team_1ID, team_2ID, COUNT(*) AS MatchCount
    FROM Match
    GROUP BY team_1ID, team_2ID
    ORDER BY MatchCount DESC
    LIMIT 1;


5. Given two teams as input, success rate of Team1 against Team2.

   : SELECT team_1ID, team_2ID, 
       (COUNT(CASE WHEN team_1runs > team_2runs THEN 1 END) / COUNT(*)) AS SuccessRate
     FROM Match
     WHERE team_1ID = <team_1ID> AND team_2ID = <team_2ID>;


Create 2 more queries on your own

6. Top 5 Players by Total Runs.
   
   : SELECT player_name, total_runs
    FROM Player
    ORDER BY total_runs DESC
    LIMIT 5;

7. Stadiums and Number of Matches Held.

   : SELECT s.stadium_name, COUNT(m.match_id) AS MatchesHeld
    FROM Stadium s
    LEFT JOIN Match m ON s.stadium_id = m.stadium_id
    GROUP BY s.stadium_name;


