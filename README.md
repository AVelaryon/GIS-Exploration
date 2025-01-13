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

 *Updated* Converted Completed Project ($\approx$) Location Description to Lat. & Lon. coordinates using `re` and `geopy`.
 The size of the bubble represents the `approved_cost_change` for each Completed Capital Projects, highlighting an extreme or, relatively, negligible under-estimation of Capital Project costs. Many of the *extreme,* *under-estimated* Completed Capital Projects are located in Long Island (specifically along the coast), in major cities like Buffalo, NY, or more inland around rural areas. These extreme, under-estimated project costs are more accentuated upon the completion of the project. The size of the bubble represents the `current_award_amount` costs of the project:
 ![Actual Project Costs](https://github.com/user-attachments/assets/79f63cb3-1149-4e5d-970b-8da9174cd860)
Of course, all of this is contingent on the type of project (i.e. `type_of_work`)...
According to [World Population Review](https://worldpopulationreview.com/us-counties/new-york), larger project costs occurs in cities with a high population density such as Buffalo, Syracuse, Albany, and anywhere near NYC

## **Funds**: A Cost Risk Problem
I should first note that the dataset (i.e., [NYS Open Data](https://dev.socrata.com/foundry/data.ny.gov/rz8t-4kmq)) has 1,932 observations, consisting of project information, namely `major_pin`, `contract_number`, `region`, `project_title`, `project_status`, `status`, `bid_opening_date`, `federal_funding`, `state_funding`, `local_funding`, `type_of_work`, `public_friendly_description`, `contract_award_date`, `contract_award_amount`, `approved_cost_changes`, `current_award_amount`, `estimated_or_actual_completed_date`, `schedule_performance`, `cost_performance`, `in_future_development_start_date`, `construction_start_date`, `construction_end_date`, and `construction_amount`. Many of the features are useless, as they don't have any measurable/discernable influence on the output of interest (i.e., `current_award_amount`) such as `major_pin`, `contract_number`, etc and, thus, were promptly removed from the dataset. `construction_start_date`, `construction_end_date`, and `construction_amount` were also removed since the features had a plethora of missing values, making imputation infeasible/intractable. `contract_award_amount` had 1,358 missing values, resulting in a dataset of length 574. And of the 574 observation, 225 of them had a *Completed Project* `status` (*I will try probabilistic imputation, albeit will incur bias*)

I extracted geographic information pertaining to project location using Python's `re` and `geopy` modules, creating new features of the `region` categorical feature: `latitude` and `longitude`. Moreover, `type_of_work` feature was re-categorized using the frequency of unique words, resulting in categories "Highway", "Traffic", "Drainage", and "Other". Subsequently, resampling was performed using *Imbalanced* Learn's `SMOTEN`, resulting in 232 observations.
Proposed Models: 
* `RandomForestRegressor`
* `SVR`
* Gaussian Process Regression
* Neural Network
* Monte Carlo Simulation 

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

***Insufficient Data***: **Dataset contains 232 observations**

** Monte Carlo Simulation**: Design of Experiment

Using the preprocessed dataset, my interest is the annual project cost that ensures the success of all projects with a probability of 95%. Given the nature of the dataset, the project cost elements are the regions, each consisting of the expected `contract_award_amount` and maximum `current_award_amount`. Each project cost element is Gaussian, consistent with the probability distributions corresponding to the cost of the `type_of_work` categorical variables. For each cost element, a random sample is draw from their respective probability distribution, defined entirely by the expected `contract_award_amount` and its deviation from the maximum `current_award_amount`, then summed, equaling the total annual project cost

For a **95% success probability** of all *232* projects, NYS DOT annual project budget must be **$365,327,161.24**.
![MC Simulation](https://github.com/user-attachments/assets/105836bd-3282-49b6-9722-c0662a9538bc)


### Endnotes and Updates
* Found an API [NYS Open Data](https://dev.socrata.com/foundry/data.ny.gov/rz8t-4kmq). Requires Pre-processing.
* I'm currently in the **model development stages**
