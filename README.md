# **GIS-Exploration**: Thoughts and Action plan
~~Investigating GIS NYS Disadvantage Community (DAC) dataset (and other datasets provided by [Geographic Information Gateway](https://opdgig.dos.ny.gov/search))~~. I wish to determine how geographic data can info decision-making and appropriate use-cases regarding transportation. This project aims to answer the following questions:
* Given all statewide projects, how does GIS data inform future project costs? Or doesn't it?
  * ~It will/may limit tools use. How does that boost or reduce cost?~
   * **Ans:** Dataset doesn't provide this info.
  * How may it inform time-completion of projects (i.e. how does geography affect the time to complete a project)?
  * What factors/possibilities may impede its timely completion?
* What features in GIS data contribute the most to the uncertainty of estimated costs of projects?
  * Once determined, we can't prevent it; we can only account for it.
![Converted Completed Project (Approx) Location to Lat. & Lon.](https://github.com/user-attachments/assets/8634f195-4f47-44f8-90c5-940764788179)

 *Updated* Converted Completed Project ($\approx$) Location Description to Lat. & Lon. coordinates, using `re` and `geopy`.
 The size of the bubble represents the `approved_cost_change` for each Completed Capital Projects, highlighting an extreme or, relatively, negligible under-estimation of Capital Project costs. Many of the *extreme,* *under-estimated* Completed Capital Projects are located in Long Island (specifically along the coast), in major cities like Buffalo, NY, or more inland around rural areas. These extreme, under-estimated project costs are more accentuated upon the completion of the project. The size of the bubble represents the `actual_completed_project_award` costs of the project:
 ![Actual Project Costs](https://github.com/user-attachments/assets/79f63cb3-1149-4e5d-970b-8da9174cd860)
Of course, all of this is contingent on the type of project (i.e. `type_of_work`)...
According to [World Population Review](https://worldpopulationreview.com/us-counties/new-york), larger project costs occurs in cities with a high population density such as Buffalo, Syracuse, Albany, and anywhere near NYC
 
## Determine the variables, required data, and **necessary** and **sufficient** assumptions (i.e., constrain assumptions)
Firstly,
* Do I truly require GIS data, if the purpose is forecasting cost?
  * Would Latitude and Longitude suffice?
 
I will include all data provided. Many variables like site location, project type, latitude, longitude, elevation, construction schedule variance (categorical and numeric), contract award cost (projected cost), current contract cost (final amount), etc. seem very relevant...

## **Funds**: A Cost Risk Problem
Monte Carlo method would be the best method to approach/handle this [Monte-Carlo Based Method for Cost Overruns](https://www.witpress.com/Secure/ejournals/papers/SSE060221f.pdf) In a similar fashion, let's consider `type_of_work`(?) to be cost elements (or maybe `region`)...
# Summary
This project is intended to develop a familiarity with using GIS data, ascertaining it's utility, and develop/formulate ways in which GIS data may inform project costs and prevent project delays. Each question itemized above will be struckthrough, indicating an answered question, followed with a summarized answer. 
### Endnotes and Updates
* Found an API [NYS Open Data](https://dev.socrata.com/foundry/data.ny.gov/rz8t-4kmq). Requires Pre-processing.
* Removed construction features; imputation isn't possible. Overall, many of the model features, like type_of_work, are poorly categorized, as it lacked consistent categories. I'll have to review each cat. and create new cats. Since many of the completed projects involved repairs on long stretches of road, features like region, and some info in project title (once it's cleaned) will have to serve as comprehensive GIS data 
* *Updated Completed Project location data*
* Finalized Categories for `type_of_work`: Bridge|Pavement|Highway|Traffic|Guiderail|Culvert|Drainage|Vegetation|Other
