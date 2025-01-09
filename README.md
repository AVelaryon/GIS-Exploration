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
| region	| 0.251807 |	0.177474 |	0.330369	| 0.152896 |
| federal_funding	| 0.078458	| 0.053866	| 0.105341	| 0.051475 |
| state_funding	| 0.062875 |	0.045097	| 0.081580	| 0.036482 |
| local_funding	| 0.062945 |	0.045879	| 0.081744	| 0.035866 |
| type_of_work	| 0.104305	| 0.073766	| 0.137792	| 0.064026 |
| month	| 0.128814	| 0.093242	| 0.164792	| 0.071550 |
| day	| 0.154680	| 0.107081	| 0.203756	| 0.096675 |
| year	| 0.344071	| 0.243379	| 0.467036	| 0.223657 |
| latitude	| 0.151172	| 0.103780	| 0.204678	| 0.100898 |
| longitude	| 0.127931	| 0.093502	| 0.166442	| 0.072940 |



** Monte Carlo Simulation**: Design of Experiment

Using the preprocessed dataset, my interest is the annual project cost that ensures the success of all projects with a probability of 95%. Given the nature of the dataset, the project cost elements are the regions...
$^{1}$ in the works

### Endnotes and Updates
* Found an API [NYS Open Data](https://dev.socrata.com/foundry/data.ny.gov/rz8t-4kmq). Requires Pre-processing.
* I'm currently in the **model development stages**
