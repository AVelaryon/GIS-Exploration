# **GIS-Exploration**: Thoughts and Action plan
~~Investigating GIS NYS Disadvantage Community (DAC) dataset (and other datasets provided by [Geographic Information Gateway](https://opdgig.dos.ny.gov/search))~~. I wish to determine how geographic data can info decision-making and appropriate use-cases regarding transportation. This project aims to answer the following questions:
* Given all statewide projects, how does GIS data inform future project costs? Or doesn't it?
  * It will/may limit tools use. How does that boost or reduce cost?
  * How may it inform time-completion of projects (i.e. how does geography affect the time to complete a project)?
  * What factors/possibilities may impede its timely completion?
* What features in GIS data contribute the most to the uncertainty of estimated costs of projects?
  * Once determined, we can't prevent it; we can only account for it.
## Determine the variables, required data, and **necessary** and **sufficient** assumptions (i.e., constrain assumptions)
Firstly,
* Do I truly require GIS data, if the purpose is forecasting cost?
  * Would Latitude and Longitude suffice?\
I will include all data provided. Many variables like site location, project type, latitude, longitude, elevation, etc. seem very relevant...
## Data Aggregation
Potential approach:
* If the interest is accounting for uncertainty of initial cost estimates, appending initial cost and final cost successively could result in **time** being the model driver and, consequently, contributing the most uncertainty, which doesn't say anything about geography rather *we need more time* (perhaps that's the answer, but why do they need more time and how could we account for that in advance?). And, between each observation (i.e., initial and final cost), GIS data of location won't change, but collectively (i.e., over all projects) may "say something" about the location and geographical features (?).
## **Funds**: A Cost Optimization Problem (?)
How could we tackle this? 
# Summary
This project is intended to develop a familiarity with using GIS data, ascertaining it's utility, and develop/formulate ways in which GIS data may inform project costs and prevent project delays. Each question itemized above will be struckthrough, indicating an answered question, followed with a summarized answer. 
### Endnotes and Updates
* [GIS Exploration](#gis-exploration) Upon inspection, DAC certainly is informative... for a different problem. Extracting [NYS DOT Completed Projects](https://www.dot.ny.gov/projects) would be most appropriate here but will become quite taxing, as it would require a string of url requests **within url requests**. Nevertheless, this is the best option. 
