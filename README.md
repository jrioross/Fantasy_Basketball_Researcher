# Fantasy_Basketball_Researcher

## Table of Contents

- [Motivation](#Motivation)
- [Technologies](#Technologies)
- [Problems & Hurdles](#Problems-&-Hurdles)
  * [Getting the Data](#Getting-the-Data)
    + [Players and IDs](#Playes-and-IDs)
    + [Calling timeout](#Calling-timeout)
  * [Normalizing the Data](#Normalizing-the-Data)
    + [NanNanNaNa, Hey, Hey, Good-bye: Calculating z-scores](#nannannana-hey-hey-good-bye-calculating-z-scores)
    + [Quantity & Quality: The Percent-Volume Problem](#quantity--quality-the-percent-volume-problem)
    + [The Less-Is-More Problem](#The-Less-Is-More-Problem)
    + [Overall (and eventually Overmost) Value](#Overall-and-eventually-Overmost-Value)
  * [Future-Me Problems](#Future-Me-Problems)
    + [Building the Punt Function](#Building-the-Punt-Function)
    + [Opponent Rater](#Opponent-Rater)
    + [The Backpack Problem: Optimum Draft by Draft Position](#The-Backpack-Problem-Optimum-Draft-by-Draft-Position)
 - [Link to the Dashboard](#Link-to-the-Dashboard)

## Motivation

I play a lot of fantasy basketball—and fantasy sports in general. Broadly speaking, sports function as a statistical petri dish, and sports enthusiasts distill ridiculous amounts of data on a regular basis. The brilliance of fantasy sports lies in giving the sports enthusiast an outlet for their sports knowledge via competitive decision-making. Within this context, an impressive range of political and economic scenarios arise (for instance, negotiating league rules, negotiating trades, and weighing team need against overall player values in a draft), which lend to a richer game experience that goes beyond the brutish, beer-and-brat-bro culture typically associated with fandom.

The structure of fantasy-basketball *category* leagues especially interests me here, over against fantasy football leagues or fantasy-basketball *points* leagues. Fantasy basketball leagues are typically played in a 9-category format, where the categories are:

  1.	Points scored (*PTS*)
  2.  Field goal percentage (non-free-throw shots made / non-free-throw shots attempted) (*FG%*)
  3.	Free throw percentage (free throws made / free throws attempted) (*FT%*)
  4.	Three-pointers made (*3PM*)
  5.	Rebounds (*REB*)
  6.	Assists (*AST*)
  7.	Steals (*STL*)
  8.	Blocks (*BLK*)
  9.	Turnovers (you want the fewer of these) (*TO*)

In the typical 9-category league, the user acts as a "team manager" who drafts a team of 13 or 14 players (with certain positional requirements based off a typical basketball roster construction). Each week, those players collect real-game statistics in the categories listed above, while an opponent’s roster also acquires statistics in those categories. If your team has better statistics in 5 or more categories at the end of the week, then your team wins; otherwise, you lose or tie (though ties are rare, since they require tying in a specific statistical category and then splitting the remaining categories).

This structure means that the fantasy-basketball player has a lot of freedom in building a winning roster. While a roster full of famous high scorers is often desirable, it’s not the only way to win. You could build a team that regularly wins rebounds, assists, steals, blocks, and turnovers, and that might get you to a championship. For similar reasons, trades in category leagues entail negotiation of which categories are important to each manager—a “trash and treasure” conversation rather than simply two people guessing about future value.

All of this means, however, that more sophisticated tools are needed for comparing player values and category contributions. In fantasy football, you can say, “This guy averages 15 fantasy points per week, and that guy averages 13 fantasy points per week,” and barring some weighing of positional value, the decision-making isn’t extensive. In fantasy basketball, on the other hand, one has to determine, for instance, whether one player’s 1.6 steals per game are more valuable to your team than another player’s 8.5 rebounds per game. And how does one make an overall determination across categories so that they can say, “Player X is better than Player Y”? Beyond that, if one wants to add a player who can contribute in one or more specific categories, how can they focus just on those categories to determine player value while ignoring (“punting”) the other categories?

My project therefore attempts to provide a dashboard research tool for 9-category fantasy basketball. There are very few tools that currently offer these resources, and the ones that do are primarily in list/grid format without much graphical insight. Ideally, this project will serve as a prototype for a future app or website.

## Technologies

I use Python 3 within a Jupyter Notebook for ETL, where the "L" in this case amounts to exporting some csv files for the dashboard. I'll admit from the outset that I much prefer working in Python to dashboarding, so the work in the Jupyter notebook exceeds what was necessary for the dashboard. It does, however, lay some groundwork for building a more sophisticated, Python-based app in the future.

For the actual dashboard, I use Power BI. It's fine.

## Problems & Hurdles

### Getting the Data

![Data_Retrieval](https://github.com/jrioross/fantasy_basketball_researcher/blob/main/images/data_retrieval.png)

#### Players and IDs

Several people have developed API-like interfaces with NBA.com. For this project, I used probably the most popular of these interfaces, which is NBA-API. NBA-API has a series of commands that retrieve select batches of information from the NBA's data. These commands typically retrieve one player's data or one team's data at a time, and they do this by referencing specific player ids or team ids as assigned by NBA.com. I therefore created a dictionary of player ids and player full names, then used the player ids of this dictionary within a loop to request data for every player--specifically, getting each player's game logs for the 2020-2021 season. Those data requests were collected into a list, which was in turn converted to a dataframe.

#### Calling timeout

There was one major hiccup in this process. NBA.com has an (undisclosed) limit to the number of requests someone can make within a timeframe, so my first several attempts to run this loop timed out. I therefore had to include a line telling the loop to pause for 0.600 seconds after each call, which makes the request rate slow enough to not overrun NBA.com's server--but it also makes the overall dataframe construction take 5 - 10 minutes. To avoid waiting on this every time I want to work in Python, I saved the initial player logs dataframe to a csv, commented out the loop code, and drew from the csv for later work. During the regular season, however, I would have to run the loop query daily to gather up-to-date data.

### Normalizing the Data

![Calculations](https://github.com/jrioross/fantasy_basketball_researcher/blob/main/images/calculations.png)

#### NanNanNaNa, Hey, Hey, Good-bye: Calculating z-scores
#### Quantity & Quality: The Percent-Volume Problem
#### The Less-Is-More Problem
#### Overall (and eventually Overmost) Value

### Future-Me Problems

#### Building the Punt Function
#### Opponent Rater

![Data_Prep](https://github.com/jrioross/fantasy_basketball_researcher/blob/main/images/data_prep.png)

#### The Backpack Problem: Optimum Draft by Draft Position

## Link to the Dashboard

https://app.powerbi.com/view?r=eyJrIjoiOTAwNjcxNDUtMzY4OS00OTcyLWE3NzMtZjQ3ZTFmOTdmNzk0IiwidCI6IjEwMWRhNTg3LTE4NDMtNGY1Mi04YjhhLTE3YjA2OWM2NmQzMyIsImMiOjJ9
