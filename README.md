# Football-Coach-College-Dynasty
College Football Universe Builder

A 50-year college football universe for Football Coach: College Dynasty, designed so the right teams win, upsets feel real, and dynasties rise and fall believably.

Built by Andrew Waldman in collaboration with Claude (Anthropic's AI) as the technical partner.

The challenge

Football Coach: College Dynasty (FCCD) lets players load a custom "universe" with every team, conference, coach and player, plus recruiting classes for future seasons. The default files don't reflect real college football. Lesser programs end up with star players, preseason polls look nothing like reality, and the long-term simulation drifts into strange outcomes.

The goal was a universe that:

Starts the season looking like real college football, matching the actual AP preseason Top 25.
Gives every team a realistic identity: strong offense, strong defense, or neither.
Ties program strength to real-world money, which is the best real predictor of success.
Produces 50 years of believable recruiting classes that flow to the right schools.
Keeps working decades into the future, not just in year one.
My role

I led the project end to end:

Set the requirements. I defined what "realistic" meant and held standing rules, such as the preseason poll having to match the real AP Top 25 exactly.
Supplied the domain knowledge. That covered conferences, rivalries, recruiting geography, school identities and NIL budgets.
Ran the simulations and diagnosed problems. I played seasons, spotted unrealistic outcomes, and traced them to root causes.
Validated every change against real-world benchmarks before accepting it.

Claude wrote the Python scripts and ran the statistical modeling under my direction.

The method

The game's internal rules aren't published, so the first step was reverse-engineering them from simulation data:

Game mechanic	What we learned
Preseason poll	Driven by the average rating of each team's top 11 offensive and top 11 defensive players. The model fit with R ≈ 0.997.
Program prestige (1–10)	Controls budget, NIL cap ($3M–$21M), boosters, and expected ranking.
Player potential	Sets how fast a player grows, not his ceiling.
Scheduling	Out-of-conference weeks pair whole conferences by prestige order, and rivalries pull specific teams out of those weeks.

With the rules understood, the universe was tuned in layers.

Problems solved
1. Preseason poll matches reality: 25 of 25

Problem: The game's preseason Top 25 bore little resemblance to the real AP poll. Fix: I used the reverse-engineered poll formula to compute each team's target strength, then made small, targeted adjustments to starters' ratings until every AP team landed in its exact slot. Result: The in-game preseason poll matches the real AP Top 25, 25 out of 25.

2. Team identity on both sides of the ball

Problem: Teams that are elite on defense but average on offense, or the reverse, need to play that way. Fix: Offensive and defensive talent were fit separately to SP+ ratings, a respected analytics measure. Result: Each unit correlates about 0.995 with real-world SP+.

3. Prestige tied to money

Problem: Prestige ratings didn't reflect the financial gap between programs. Fix: Prestige was re-based on reported 2026 NIL budgets for 68 power-conference programs. Teams were moved only when they were clearly out of line, and never more than one level at a time. Result: Only three true blue-bloods sit at the top tier, and spending lines up with success.

4. Good recruits signing with weak programs

Problem: In the generated classes, a recruit's interest in a program's prestige had no relationship to his talent, so stars signed anywhere. Fix: Recruit priorities were tied to potential. Elite prospects now weight prestige and NIL heavily, and lower-rated prospects weight playing time and staying close to home. Result: The correlation between talent and prestige-seeking went from about 0.00 to 0.84.

5. Group of Five players winning the Heisman

Problem: Long-term sims kept producing Heisman winners from small conferences. Diagnosis: Elite recruits signed with powerhouses, couldn't get on the field, transferred down to smaller programs, and grew into superstars there. Fix: Elite potential was made rare, with a target curve by class rank so that only the top 0.5% of each class gets a true elite ceiling. Result: Elite-potential recruits dropped from 592 per class to about 21. A player who transfers down still becomes a good starter, not a Heisman favorite.

6. Real recruiting geography

Problem: Recruits had random hometowns, and the game sometimes didn't recognize them. Fix: Recruits are placed using a 42-region recruiting map, weighted by how much talent each region really produces. Hometowns come from real zip codes, and each region has its own position mix. Result: Regional distribution matches the target within about 0.2%, and top prospects concentrate in real hotbeds like Texas, Southern California and Florida.

7. Built-in realism
Rivalries: 359 rivalry pairings, with frequencies checked against the most-played series in college football history. Every team has at least one schedulable rival.
Busts: About 56 highly rated recruits per class arrive underdeveloped and never pan out, as in real life.
Upsets: About 15% of ranked teams lose to unranked opponents, and about 14% of games are decided by one score.
By the numbers
	
Players	~10,900
Teams and coaching staffs	138
Conferences	10
Rivalries	359
Recruiting classes	50 (2026–2075)
Recruits per class	2,750
Preseason AP match	25 / 25
Repository contents
/scripts
  pollcalc.py           Computes poll points from team ratings
  apfit.py              Fits the preseason poll to the real AP Top 25
  position_balance.py   Corrects rating imbalances by position
  pipelines.py          42-region recruiting geography model
  busts.py              Generates the bust tail in each class
/recruiting
  2026.json … 2075.json 50 generated recruiting classes (fictional players)
/docs
  mechanics.md          Full notes on the reverse-engineered game mechanics

About the data: The recruiting classes are entirely fictional and included here. The base universe file was built from a personal ratings export and real rosters, so it is not included. The scripts are designed to run on your own export.

Recommended game settings
Difficulty: Normal. Harder settings penalize auto-recruiting and computer playcalling.
Out-of-conference schedule: Fluid. The rivalry slots are built for it.
Remaining player generation: Standard.
Potential randomization: Off. Development is driven by the file.
What this project demonstrates
Directing AI on a complex, multi-month technical build. That meant setting goals, making judgment calls, and holding the work to a standard.
Systems thinking. Undocumented rules were reverse-engineered from observed behavior.
Data-driven problem solving. Each fix started with a diagnosis and ended with a measured result.
Quality control. Every change was validated against real-world benchmarks.

This is a personal, non-commercial fan project. It is not affiliated with or endorsed by the makers of Football Coach: College Dynasty, EA Sports, the NCAA, or any university. Team names are used for identification only.
