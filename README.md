# README.md

## Prelim Instructions
### Libraries Necessary for Project:
- pandas
- numpy
- scipy.stats
- ipynb
- matplotlib.pyplot
### Files Order of Operations
1. data_cleaning_final.ipynb
2. establishing_functions.ipynb
3. Any analysis files:
   - cahoots_percentage_over_time
   - cahoots_correlation_analysis
   - cahoots_mean_sampling
## Data Cleaning
### User Steps
- Load CAD data into data_cleaning_final.ipynb
- Run all cells
### Cleaning Steps Taken
- Import call data from CAD
- Change Call_Created_Time to pd.datetime form
- Rename "Call_Created_Time" to "Call Time"
- Selected relevant columns for my analysis ["Call Time", "PrimaryUnitCallSign", "RespondingUnitCallSign", "InitialIncidentTypeDescription", "Disposition"]
- Removed rows with "InitialIncidentTypeDescription" are empty, I need that rows with that info for further analysis
- Removed rows where both "PrimaryUnitCallSign" and "RespondingUnitCallSign" are empty
- Renamed columns as follows to increase ease of analysis for me {"PrimaryUnitCallSign": "Call Sign", "InitialIncidentTypeDescription": "Reason for Dispatch", "RespondingUnitCallSign": "2 Call Sign"}
- Filtered dispositions that implied no action was taken. This removes almost all the calls labeled 'CAHOT'
- Set the file to automatically save to the current folder after cleaning for easy transfer to next file.
## Prelim Global Variables
### Location:
- establishing_functions.ipynb
### What I did:
- Load cleaned dataset from data_cleaning_final
- Set call signs I will be searching for during analysis. Named as both target_call_signs and cahoots_call_signs. 
- Manually find first and last occurrence of the three call signs
- Defined calculate_counts, a helper function that is used in all my other files. 
  - Input:
    - table: a dataframe of a selection of calls from clean_cad 
    - call_signs: a list of call signs 
  - Output:
    - A table with monthly counts of total calls, and total count of calls where a labeled call sign appeared
## Analysis files
### cahoots_percentage_over_time.ipynb
- Plotted Monthly Percent of Cahoots Calls out of total CAD calls. Labeled first occurrence of each new call sign
- Plotted each individual call sign percent as part of the whole
- Plotted each individual percent out of the total cahoots calls
- Found difference in average percent between 3J78 and 4J79
- Plotted a stacked call sign count graph as a percentage of a whole
### cahoots_correlation_analysis.ipynb
- Plotted Total CAD calls vs Cahoots Calls monthly count
- Plotted a zoomed in Monthly total Cahoots Call Counts
- Plotted count of each individual Call sign
- Plotted total monthly calls vs total monthly cahoots calls to check for correlation.
- After no correlation was seen added dimension of time period. Distinct groupings can be seen with no variation due to total calls.
### cahoots_mean_sampling.ipynb
- Assigned each call in CAD dataset a color based on time period
- Randomly selected calls from given time periods (with replacement) and found the percentage of those calls for each test.
- Plotted those average percentages on a histogram w/ mean.