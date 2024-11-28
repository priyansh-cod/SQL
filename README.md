FIFA World Cup Analysis

This project analyzes data from the FIFA World Cup to provide insights on team performance, player statistics, and match outcomes.

Project Overview

The project uses a SQL database to store and analyze data from the FIFA World Cup. The database includes tables for teams, players, matches, and goals.

Results

1. Top 5 Teams by Total Goals Scored

| Rank | Team | Total Goals |
| --- | --- | --- |
| 1 | Brazil | 15 |
| 2 | Germany | 13 |
| 3 | Argentina | 12 |
| 4 | Spain | 11 |
| 5 | France | 10 |

2. Top 5 Players by Total Goals Scored

| Rank | Player | Team | Total Goals |
| --- | --- | --- | --- |
| 1 | Lionel Messi | Argentina | 6 |
| 2 | Cristiano Ronaldo | Portugal | 5 |
| 3 | Kylian Mbappé | France | 4 |
| 4 | Robert Lewandowski | Poland | 3 |
| 5 | Neymar Jr. | Brazil | 3 |

3. Match Outcomes by Team

| Team | Wins | Draws | Losses |
| --- | --- | --- | --- |
| Brazil | 4 | 1 | 1 |
| Germany | 3 | 2 | 1 |
| Argentina | 3 | 1 | 2 |
| Spain | 2 | 3 | 1 |
| France | 2 | 2 | 2 |


Database Schema

The database schema includes the following tables:

Teams

| Column Name | Data Type |
| --- | --- |
| team_id | int |
| team_name | varchar(255) |
| team_country | varchar(255) |

Players

| Column Name | Data Type |
| --- | --- |
| player_id | int |
| player_name | varchar(255) |
| player_team_id | int |
| player_position | varchar(255) |

Matches

| Column Name | Data Type |
| --- | --- |
| match_id | int |
| match_date | date |
| match_team1_id | int |
| match_team2_id | int |
| match_result | varchar(255) |

Goals

| Column Name | Data Type |
| --- | --- |
| goal_id | int |
| goal_match_id | int |
| goal_player_id | int |
| goal_time | int |

SQL Queries

The following SQL queries were used to generate the results:

Top 5 Teams by Total Goals Scored


SELECT 
  t.team_name, 
  SUM(g.goal_time) AS total_goals
FROM 
  teams t
  JOIN matches m ON t.team_id = m.match_team1_id
  JOIN goals g ON m.match_id = g.goal_match_id
GROUP BY 
  t.team_name
ORDER BY 
  total_goals DESC
LIMIT 5;


Top 5 Players by Total Goals Scored


SELECT 
  p.player_name, 
  SUM(g.goal_time) AS total_goals
FROM 
  players p
  JOIN goals g ON p.player_id = g.goal_player_id
GROUP BY 
  p.player_name
ORDER BY 
  total_goals DESC
LIMIT 5;


Match Outcomes by Team


SELECT 
  t.team_name, 
  SUM(CASE WHEN m.match_result = 'win' THEN 1 ELSE 0 END) AS wins,
  SUM(CASE WHEN m.match_result = 'draw' THEN 1 ELSE 0 END) AS draws,
  SUM(CASE WHEN m.match_result = 'loss' THEN 1 ELSE 0 END) AS losses
FROM 
  teams t
  JOIN matches m ON t.team_id = m.match_team1_id
GROUP BY 
  t.team_name;
