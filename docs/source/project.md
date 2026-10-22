DALLAS STARS 2026-27 SEASON 
PERFORMANCE FORECASTING MODEL
Mathematical Models Semester Project Proposal
Business Customer: Dr. Wilson
Team Members and Roles
Derek Nguyen - Lead
Yakov Gavriyelov - Project Planner
Ankit Karki - Quality Assurance Lead
Proposal Date: October 6, 2026
Final Presentation Date: November 16, 2026
Decision Question
Given the Dallas Stars' 2025-26 offensive and defensive performance, how would changes in scoring 
strength, defensive/goaltending strength, and selected roster personnel affect the distribution of the 
team's 2026-27 regular-season wins, standings points, playoff-level performance, and likely Central 
Division standing?
1. Executive Summary and Business Objective
This project will develop a probabilistic forecasting model for the Dallas Stars using completed NHL 
data through the end of the 2025-26 regular season. The model will estimate Dallas goals scored and 
goals allowed at the game level, simulate complete 82-game seasons thousands of times, and measure 
how the projected season changes under controlled offensive, defensive, and roster scenarios.
The primary model will combine Poisson goal-count submodels with Monte Carlo simulation. The 
primary response variable will be Dallas regular-season standings points. Secondary outputs will 
include wins, regulation losses, overtime/shootout losses, goal differential, probability of reaching 
selected point thresholds, and a probability-based estimate of Central Division standing. The project 
will not attempt to predict every NHL team game-by-game; historical Central Division standings will 
instead be used to translate a simulated Dallas point total into a likely range of division outcomes.
To preserve the integrity of the forecast, the model-development data cutoff will be the conclusion of 
the 2025-26 regular season. The official 2026-27 Dallas roster may be used to define realistic personnel 
scenarios, but 2026-27 regular-season game results will not be used to fit the forecasting model.
2. Scope, Research Questions, and Success Criteria
Primary research question:
How sensitive is the Dallas Stars' projected 2026-27 regular-season 
performance to changes in offensive scoring, defensive/goaltending 
performance, and selected roster personnel?
The project will answer the following measurable subquestions:







What probability distributions reasonably describe Dallas game-level goals for and goals against?
What 82-game point distribution is produced by a baseline model calibrated to 2025-26?
How much does the projected point distribution change when offensive scoring strength changes 
while defense is held constant?
How much does the projected point distribution change when goals allowed changes while offense 
is held constant?
How do selected player-removal, player-addition, or player-availability scenarios alter the offensive 
rate and the simulated season distribution?
How well would the modeling approach have predicted the known 2025-26 season if it had been 
calibrated only on 2024-25 information?
Given historical Central Division standings, what division-finish range is associated with the 
simulated Dallas point totals?
Success criteria:






Produce explicit mathematical formulas for all core submodels and the integrated season 
simulation.
Use reproducible, cited data from NHL.com and Hockey-Reference rather than subjective ratings.
Generate graphical output that communicates distributions, sensitivity, and model error.
Validate the model against a known season and document prediction error.
Perform QA tests on data reconciliation, distributional assumptions, code outputs, and final figures.
State limitations and sources of uncertainty rather than presenting a single forecast as certain.
3. Team and Roles
Member Role
Primary Accountability
Planned Responsibilities
Derek
Lead
Keep the team on task and 
accountable; ensure group 
processes and the contract are 
followed.
Coordinate group decisions; resolve task 
ownership issues; lead business-customer 
communication; ensure participation and 
readiness for submission/presentation.
Yakov
Project Planner
Own and maintain the project 
plan; track tasks, milestones, 
dependencies, and corrections.
Maintain the schedule in the proposal; track 
data/model/report/presentation work; 
coordinate deadlines with Derek; update 
assignments if the plan changes.
Ankit
Quality 
Assurance Lead
Own the test plan and verify 
calculations, model 
performance, documentation, 
and presentation quality.
4. Mathematical Modeling Plan
Create QA checklist; verify source-to-dataset 
reconciliation; test Poisson assumptions; audit 
Monte Carlo logic; run backtest/error checks; 
inspect final tables/graphs/citations.
The project will be organized as several linked submodels. This allows the team to change one 
component at a time and observe the effect on the final season forecast.
4.1 Baseline Offensive Goal Model
Let X_i be Dallas goals scored in game i. The starting model is
X_i ~ Poisson(λ_GF)
Using official 2025-26 team totals, Dallas scored 273 goals in 82 games, giving the baseline estimate
λ_GF = 273 / 82 ≈ 3.329 goals per game.
The team will use the game log to compare the empirical goal-count distribution with the fitted Poisson 
distribution. Mean-versus-variance behavior, observed versus expected frequencies, and a goodness-of
fit diagnostic will be recorded. If the data show material overdispersion, the team will document the 
failure of the simple Poisson assumption and evaluate a planned fallback such as a negative-binomial 
or segmented Poisson model.
4.2 Baseline Defensive Goal Model
Let Y_i be goals allowed by Dallas in game i. The starting model is
Y_i ~ Poisson(λ_GA)
Dallas allowed 222 goals in 82 games in 2025-26, so
λ_GA = 222 / 82 ≈ 2.707 goals allowed per game.
Defensive sensitivity will be modeled by changing λ_GA while holding λ_GF fixed. Goaltending statistics 
such as save percentage and goals-against average will be used as supporting variables and for 
scenario justification, not as separate points added directly to the standings model.
4.3 Offensive and Defensive Sensitivity Submodels
The model will intentionally vary one side of performance while keeping the other fixed. Planned 
sensitivity levels are ±5%, ±10%, and ±15% around the baseline rates. For example:
λ_GF(s) = λ_GF,0(1 + s),    λ_GA(d) = λ_GA,0(1 + d),
where s and d are the chosen offensive and defensive percentage changes. These submodels will show 
the marginal effect of scoring or defending better/worse without confounding both changes at once.
4.4 Roster/Player Impact Submodel
Selected player scenarios will translate individual scoring production into a change in the team scoring 
rate. For a simple forward replacement scenario, an initial adjustment will take the form
λ_GF,new = λ_GF,0 - g_out + g_in,
where g_out and g_in are estimated per-team-game goal contributions for the outgoing and 
incoming/replacement player after normalizing for games played and expected role. The group will 
avoid simply subtracting all of a departing player's goals without replacement; a realistic replacement 
contribution will be included. Player goals, assists, shots, shooting percentage, games played, and 
average time on ice will be used to justify the scenario. If a defensive-player scenario is selected, the 
group will use team goals-against changes or on-ice/defensive metrics rather than treating a 
defenseman's offensive points as defensive value.
4.5 Regulation, Overtime/Shootout, and Season Simulation
For each simulated game, independent goal counts will be generated from the offense and defense 
models. A game with X_i > Y_i is a Dallas win; X_i < Y_i is a regulation loss. If the simulated regulation 
outcome is tied, an overtime/shootout outcome will be sampled using an empirically estimated Dallas 
probability from historical tied games. Standings points will be assigned according to NHL structure: 
two points for a win, one point for an overtime/shootout loss, and zero for a regulation loss.
One simulated season contains 82 games. Each scenario will be repeated for at least 10,000 simulated 
seasons. The model will save the distribution of wins, losses, overtime losses, standings points, and goal 
differential. A fixed random seed will be used for reproducibility in QA runs.
4.6 Standings Translation Submodel
The project will not simulate every opponent's full season. Instead, completed Central Division 
standings from full 82-game seasons (2021-22 through 2025-26) will be used to relate point totals to 
division rank and playoff-level thresholds. For each simulated Dallas point total, the team will estimate 
the historical frequency or range of division positions associated with comparable point totals. This 
yields probability-based statements such as “top-three Central likelihood” rather than an unjustified 
exact-rank claim.
4.7 Backtest / Validation Model
The QA backtest will mimic a prior-year forecast. The model will first be calibrated using only 2024-25 
Dallas information, then used to predict a distribution for 2025-26. The predicted distribution will be 
compared with the known 2025-26 result (50-20-12, 112 points). Primary validation measures will 
include absolute point error, whether the actual point total falls inside the simulated prediction 
interval, and discrepancies in wins/losses/overtime losses. The team will document any model revision 
made after the backtest.
5. Data Plan and Required Reference Data
Data cutoff for model fitting: end of the 2025-26 regular season. 2026-27 results are excluded from 
fitting. The following fields are required.
Dataset
Fields Needed
Use in Model
Primary Source
2025-26 Dallas team 
season totals
GP, W, L, OT, points, GF, GA, 
GF/GP, GA/GP, PP%, PK%, 
shots/game, shots against/game, 
faceoff %
Baseline λ values; descriptive 
context; special-teams/supporting 
variables
NHL.com Team Stats
2025-26 Dallas game 
log
Game date, opponent, 
home/away, GF, GA, 
regulation/OT/SO result, shots, 
PPG/PPO, opponent shots and 
power-play results; advanced 5
on-5 fields where available
Empirical scoring distributions; 
Poisson fit tests; OT/SO frequency; 
variance; optional home/away 
submodel
DallasStars.com / 
NHL.com
Hockey-Reference 
Dallas Team Gamelog
2025-26 Dallas skater 
statistics
Player GP, goals, assists, points, 
shots, shooting %, PPG, TOI/GP; 
selected advanced fields if used
Roster-change scenarios and 
normalized player contribution 
estimates
NHL.com Skater Stats / 
Dallas player profiles
2025-26 Dallas goalie 
statistics
Goalie GP/GS, W-L-OT, shots 
against, saves, GA, SV%, GAA, 
shutouts
Defensive/goaltending scenario 
justification and QA checks
NHL.com Goalie Stats / 
Dallas player profiles
2024-25 Dallas team 
totals and game log
Same core team/game fields as 
2025-26
Backtest calibration dataset
NHL.com and Hockey
Reference
2021-22 through 2025
26 Central Division 
standings
Team, GP, W, L, OT, points, point 
%, GF, GA, rank/playoff status
Translate simulated Dallas points 
into probable 
rank/top-three/playoff-level 
outcomes
Hockey-Reference NHL 
season standings
2026-27 Dallas initial 
roster
Opening roster by position; 
returning players and offseason 
acquisitions
Define realistic roster scenarios 
only; not model fitting
Data-cleaning rule for shootouts: Poisson goal fitting will use hockey goals, not the artificial one-goal 
increment sometimes displayed in a final shootout score. Game-log totals will be reconciled to the 
official NHL season totals of 273 goals for and 222 goals against before parameters are estimated.
6. Planned Scenarios and Outputs
At minimum, the final analysis will report the following scenario families:
Scenario
Change
Purpose
S0 - Baseline
2025-26 Dallas scoring and goals-allowed rates 
held constant.
Measure point sensitivity to attack 
changes.
Reference distribution for all 
comparisons.
S1 - Offensive 
sensitivity
λ_GF changed by -15%, -10%, -5%, +5%, +10%, 
+15%; λ_GA fixed.
Scenario
Change
Purpose
S2 - Defensive 
sensitivity
λ_GA changed by -15%, -10%, -5%, +5%, +10%, 
+15%; λ_GF fixed.
Measure point sensitivity to 
defense/goaltending changes.
S3 - Player/roster 
scenarios
At least two realistic 
removal/addition/availability scenarios based on 
2025-26 player rates and the 2026-27 roster.
Translate personnel choices into 
changed scoring/defensive 
assumptions.
S4 - Combined 
scenario
One plausible combined offense + defense + 
roster case after individual sensitivities are 
understood.
For each scenario, planned outputs include:






mean/median standings points and 80%/95% simulation intervals
mean wins, regulation losses, and overtime/shootout losses
mean goal differential
histogram/density-style chart of simulated points
probability of 90+, 95+, 100+, 105+, and 110+ points
Provide a management-style “best 
estimate” scenario without hiding 
component effects.
estimated probability of a top-three Central Division point level and other historically meaningful 
standing ranges

difference from baseline in expected points and outcome probabilities
7. Computational and Technology Tools
The group intends to use computational tools for number crunching, simulation, data cleaning, 
graphical analysis, and reproducibility. The final mathematical definitions and conclusions will remain 
the group's work.





Python: pandas for data organization; NumPy for random sampling and vectorized Monte Carlo 
calculations; SciPy or equivalent statistical functions for probability and goodness-of-fit 
calculations; Matplotlib for graphs.
Excel or Google Sheets: project-plan tracking, source reconciliation, spot checks of formulas, and 
small summary tables.
Word/Google Docs: proposal and final written documentation.
PowerPoint/Google Slides: class presentation.
Versioned code/notebook files: preserve model inputs, random seed, scenario settings, and output 
tables so QA can reproduce results.
8. Written Documentation and Graphical Deliverables
The final group submission is expected to include the following materials, subject to Business Customer 
approval:





Problem statement and business interpretation.
Source/data description and data-cleaning notes.
Derivation and explanation of the Poisson offense and defense models.
Roster adjustment formulas and scenario assumptions.
Monte Carlo simulation logic and standings-point calculation.





Backtest and QA test plan/results.
Tables of baseline and scenario outputs.
Graphs of actual goal frequencies versus fitted distributions, simulated point distributions, 
sensitivity results, and historical points-versus-division-rank relationships.
Discussion of uncertainty, limitations, possible sources of error, and recommendations.
Appendix containing code or sufficiently detailed pseudocode and parameter tables for 
reproducibility.
9. Quality Assurance and Sources of Error
Ankit, as QA Lead, will maintain a test plan. Planned QA activities include:








Source reconciliation: confirm season totals calculated from cleaned game data agree with official 
NHL totals.
Shootout handling: verify that shootout decision goals are not treated as normal hockey goals in the 
Poisson fit.
Distribution checks: compare sample means and variances and observed versus expected count 
frequencies; document whether Poisson is adequate.
Code tests: confirm 82 games per simulated season; points equal 2W + OTL; outcome counts sum to 
82; repeated runs with a fixed seed reproduce identical outputs.
Backtest: train/calibrate on 2024-25 and compare the simulated 2025-26 distribution against the 
actual 112-point outcome.
Sensitivity sanity checks: improved offense or reduced goals allowed should not systematically 
worsen projected points under otherwise identical assumptions.
Independent spot checks: hand-calculate selected probability and point examples and compare 
them with code output.
Document/presentation QA: verify tables, labels, citations, equations, and graphs are internally 
consistent.
Known or anticipated sources of error/uncertainty include:






Goals for and goals against are not perfectly independent; game state changes behavior.
A single constant Poisson rate ignores opponent strength, injuries, travel, home/away effects, 
empty-net situations, and schedule difficulty.
Player production is not additive in a perfectly linear way because line combinations, ice time, 
coaching, power-play roles, and replacement players matter.
A player's prior-year production may not repeat because of health, aging, shooting percentage 
regression, or role changes.
Historical point-to-rank relationships are based on a limited number of Central Division seasons 
and cannot account for every opponent change.
Monte Carlo simulation quantifies uncertainty conditional on model assumptions; it does not 
eliminate model error.
Project Plan and Tentative Schedule
The schedule begins October 6, 2026 and ends with the required final presentation on November 30, 
2026. The Project Planner will maintain the working version and coordinate changes with the Lead.
Dates Milestone Primary Owner Deliverable / Exit Criterion QA / Dependency
Oct 6-9 Proposal finalization and 
Business Customer 
alignment
Derek + Yakov Proposal submitted; 
meeting/sign-off requested; 
scope locked.
Ankit checks requirements 
coverage and reference 
list.
Oct 10-13 Data acquisition and 
cleaning
Team; Yakov tracks 2024-25 and 2025-26 
team/game/player/goalie 
datasets assembled; 2026-27 
results excluded.
Totals reconcile to NHL 
sources; shootouts cleaned.
Oct 14-19 Poisson submodels, 
exploratory analysis, and 
Baseline Monte Carlo 
engine
Modeling work 
shared
Baseline lambda estimates, 
empirical distributions, fit 
diagnostics, initial graphs.
82-game season simulation 
functioning; >=10,000 seasons; 
baseline outputs saved.
Ankit records fit tests and 
flags overdispersion.
Code invariants and seed 
reproducibility tested.
Oct 20-23 Sensitivity and roster 
submodels + Backtest and 
model refinement
Team Offense/defense sensitivity grid 
plus at least two personnel 
scenarios completed.
Backtest completed; error 
metrics documented; approved 
refinements made.
Scenario inputs traced to 
cited player data.
Method changes 
documented and 
communicated.
Oct 24-27 Final model runs and 
standings translation
Team Final simulations, rank 
translation, summary tables, and 
figures completed.
Cross-run consistency and 
interpretation check.
Oct 28 Written results + first 
presentation draft
Derek coordinates; 
Yakov tracks
First complete written draft and 
first complete slide deck.
Ankit performs content, 
equation, graph, and 
citation review.
Nov 9 Revision and QA closure All Errors corrected; final 
conclusions and limitations 
approved.
QA checklist closed or 
exceptions documented.
Nov 11 Final rehearsal and 
submission package
All Timed rehearsal; final files 
checked; speaking roles 
confirmed.
Final formatting and 
reproducibility check.
Nov 16 Final class presentation All Present results, model, 
validation, limitations, and 
recommendation.
Final delivery milestone.
10. Planned Class Presentation
The presentation will be structured as a concise analytics briefing to the Business Customer and class:
1. Business question and why Dallas was selected.
2. Data sources, cutoff, and key 2025-26 baseline statistics.
3. Poisson offense/defense submodels and fit evidence.
4. Monte Carlo season simulation and NHL standings-point logic.
5. Backtest results and QA findings.
6. Offensive sensitivity, defensive sensitivity, and roster-change scenarios.
7. Projected point distributions and probable Central Division outcome range.
8. Recommendation / interpretation for the hypothetical team decision-maker.
9. Limitations and what would improve the next version of the model.
11. Change Control / “Life Happens” Plan
If a significant problem is discovered - for example, unavailable data, failure of the Poisson assumption, 
coding issues, or an unmanageable roster scenario - the team will document the issue immediately. 
Yakov will update the project plan, Derek will coordinate the team response and communicate material 
scope/deliverable changes to the Business Customer, and Ankit will document the QA impact. The team 
will not silently substitute a materially different model after proposal approval. A planned statistical 
fallback (such as a negative-binomial or segmented Poisson goal model) may be used if the Poisson fit is 
demonstrably inadequate, with the reason and validation evidence reported.
12. References and Data Sources
The following sources are sufficient to build the planned baseline, validation, scenario, and standings 
datasets. Accessed October 6, 2026 unless otherwise noted.
1. National Hockey League. “NHL Stats - Teams, 2025-26 Regular Season.” Official team-level source 
for GP, W-L-OT, points, GF, GA, GF/GP, GA/GP, PP%, PK%, shots/game, shots against/game, and faceoff 
percentage. https://www.nhl.com/stats/teams?
gameType=2&page=0&pageSize=50&reportType=season&seasonFrom=20252026&seasonTo=20252026
2. National Hockey League. “NHL Stats - Skaters, 2025-26 Regular Season.” Official player-level 
source for games played, goals, assists, points, shots, shooting percentage, power-play goals/points, time 
on ice, and other skater fields used in roster scenarios. https://www.nhl.com/stats/skaters?
gameType=2&page=0&pageSize=50&reportType=season&seasonFrom=20252026&seasonTo=20252026
3. National Hockey League. “NHL Stats - Goalies, 2025-26 Regular Season.” Official source for goalie 
GP/GS, wins, losses, overtime losses, shots against, saves, goals against, save percentage, GAA, and 
shutouts. https://www.nhl.com/stats/goalies?
gameType=2&page=0&pageSize=50&reportType=season&seasonFrom=20252026&seasonTo=20252026
4. Hockey-Reference. “2025-26 Dallas Stars Team Gamelog.” Game-level data for fitting and testing 
the goals-for/goals-against distributions and estimating overtime/shootout behavior. 
https://www.hockey-reference.com/teams/DAL/2026_gamelog.html
5. Hockey-Reference. “2024-25 Dallas Stars Team Gamelog.” Historical game-level calibration data 
for the out-of-sample backtest. https://www.hockey-reference.com/teams/DAL/2025_gamelog.html
6. Hockey-Reference. “2025-26 Dallas Stars Roster and Statistics.” Cross-check of season totals, 
player statistics, team analytics, and roster context. 
https://www.hockey-reference.com/teams/DAL/2026.html
7. Hockey-Reference. “2024-25 Dallas Stars Roster and Statistics.” Backtest season source for team 
and player baseline statistics. https://www.hockey-reference.com/teams/DAL/2025.html
8. Hockey-Reference. NHL season standings, 2021-22 through 2025-26. Central Division point totals 
and finishing positions for the standings-translation submodel. 
https://www.hockey-reference.com/leagues/
9. Dallas Stars Communications. “Dallas Stars announce initial roster for 2026-27 season.” 
September 28, 2026. Official roster source to define realistic personnel scenarios without using 2026-27 
game outcomes to fit the model. https://www.nhl.com/stars/news/dallas-stars-announce-initial-roster
for-2026-27-season-092826
10. Dallas Stars / NHL.com player profiles, 2026-27 series. Cross-check of 2025-26 player production 
and injury/role context for selected roster scenarios (e.g., Robertson, Johnston, Rantanen, Hintz, 
Oettinger). https://www.nhl.com/stars/news/
13. Proposal Approval Statement
The group requests approval to proceed with the scope, data plan, modeling approach, deliverables, QA 
plan, and schedule described above. Any material change to the agreed deliverables will be 
communicated to the Business Customer as soon as it is identified.
Business Customer / Instructor
Date
Approval / Comments:
Group acknowledgement of changes (if any):