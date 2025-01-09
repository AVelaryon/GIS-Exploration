# **GIS-Exploration**: Thoughts and Action plan
I wish to determine how geographic data can info decision-making and appropriate use-cases regarding transportation. This project aims to answer the following questions:
* Given all statewide projects, how does GIS data inform future project costs? Or doesn't it?
  * ~It will/may limit tools use. How does that boost or reduce cost?~
   * **Ans:** Dataset doesn't provide this info.
  * How may it inform time-completion of projects (i.e. how does geography affect the time to complete a project)?
  * What factors/possibilities may impede its timely completion?
* What features in GIS data contribute the most to the uncertainty of estimated costs of projects? $^{2}$
  * Once determined, we can't prevent it; we can only account for it.
![Converted Completed Project (Approx) Location to Lat. & Lon.](https://github.com/user-attachments/assets/8634f195-4f47-44f8-90c5-940764788179)

 *Updated* Converted Completed Project ($\approx$) Location Description to Lat. & Lon. coordinates, using `re` and `geopy`.
 The size of the bubble represents the `approved_cost_change` for each Completed Capital Projects, highlighting an extreme or, relatively, negligible under-estimation of Capital Project costs. Many of the *extreme,* *under-estimated* Completed Capital Projects are located in Long Island (specifically along the coast), in major cities like Buffalo, NY, or more inland around rural areas. These extreme, under-estimated project costs are more accentuated upon the completion of the project. The size of the bubble represents the `current_award_amount` costs of the project:
 ![Actual Project Costs](https://github.com/user-attachments/assets/79f63cb3-1149-4e5d-970b-8da9174cd860)
Of course, all of this is contingent on the type of project (i.e. `type_of_work`)...
According to [World Population Review](https://worldpopulationreview.com/us-counties/new-york), larger project costs occurs in cities with a high population density such as Buffalo, Syracuse, Albany, and anywhere near NYC

## **Funds**: A Cost Risk Problem
Proposed Models: 
* `RandomForestRegressor`
* `SVR`
* Gaussian Process Regression
* Neural Network
* Monte Carlo Simulation $^{1}$

Monte Carlo method would be the best method to approach/handle this [Monte-Carlo Based Method for Cost Overruns](https://www.witpress.com/Secure/ejournals/papers/SSE060221f.pdf) [Cost Overruns](https://ijisrt.com/assets/upload/files/IJISRT23APR1646.pdf)\
Each proposed model has different objectives. As a "startup" model, `RandomForestRegressor` will be used to ascertain uncertainty/importance of model features and to make projections of potential project costs based on randomized combinations of model features' values.

Using `RandomForestRegressor` with HT={`n_estimators=100`, `random_state=0`}, the *total-order permutation variable importance* (**TPVi**)

| Feature Names | TPVi |	5th |	95th | Quantile Width|
| :----: | :----: | :----: | :----: | :----: |
| federal_funding	| 0.072495	| 0.061748	| 0.083938	| 0.022190|
| state_funding	| 0.072556	| 0.057008	| 0.089305	| 0.032297 |
| local_funding	| 0.063040	| 0.054447	| 0.071941	| 0.017494 |
| type_of_work	| 0.211675	| 0.167289	| 0.258051	| 0.090762 |
| month	| 0.163776	| 0.138574	| 0.188030	| 0.049455 |
| day	| 0.147903	| 0.123540	| 0.174228	| 0.050688 | 
| year	| 0.184490	| 0.146064	| 0.222625	| 0.076561 |
| latitude	| 0.216691	| 0.183160	| 0.252752	| 0.069591 |
| longitude	| 0.274353	| 0.232364	| 0.317739	| 0.085374 |

***Insufficient Data***

** Monte Carlo Simulation**: Design of Experiment

Using the preprocessed dataset, my interest is the annual project cost that ensures the success of all projects with a probability of 95%. Given the nature of the dataset, the project cost elements are the regions...
$^{1}$ in the works

### Endnotes and Updates
* Found an API [NYS Open Data](https://dev.socrata.com/foundry/data.ny.gov/rz8t-4kmq). Requires Pre-processing.
* I'm currently in the **model development stages**
