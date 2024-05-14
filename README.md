# README.md

## data_cleaning_final.ipynb

### Loading data
- In the data_cleaning_final file add the path of the CAD dataset that was provided
- Once that is added, all of the cleaned data should auto-save to the 410 Final Project folder my project files are stored in.
- The project is stored in the master branch, download the 410 Final Project folder to run files. (I'm still learning GitHub)

### Libraries
- pandas, matplotlib.pyplot, numpy, and datetime necessary to run files

### Cleaning Steps Taken
  - Import call data from CAD
  - Change Call_Created_Time to pd.datetime form
  - Rename "Call_Created_Time" to "Call Time"
  - Selected relevant columns for my analysis ["Call Time", "PrimaryUnitCallSign", "RespondingUnitCallSign", "InitialIncidentTypeDescription", "Disposition"]
  - Removed rows with "InitialIncidentTypeDescription" are empty, I need those rows with that info for further analysis
  - Removed rows where both "PrimaryUnitCallSign" and "RespondingUnitCallSign" are empty.
  - Renamed columns as follows to increase ease of analysis for me {"PrimaryUnitCallSign": "Call Sign", "InitialIncidentTypeDescription": "Reason for Dispatch", "RespondingUnitCallSign": "2 Call Sign"}
  - Set the file to automatically save to the current folder after cleaning for easy transfer to the next file.

## cahoots_calls_over_time.ipynb

### Helper Functions:
- cahoots_call_signs:
  - A list of the cahoots call signs in Eugene that I will be analyzing in this project.

- time_filter_year:
  - A helper function to quickly filter data frames by year. Used in later analysis

- time_filter_month:
  - Another helper function used to filter times monthly given a start and end month and year.
  percent_cahoots_calls:
  - Calculates the percentage of calls where either call sign or 2 call sign contains a cahoots call sign out of the total calls

- filter_incidents:
  - Takes a data frame, column name, and list
  - returns a data frame where the columns incidents are contained in the list
  
- calc_monthly_percentages:
  - Given a data frame and a list of Cahoots call signs, it returns the percentage of Cahoots calls out of total calls by month
  - Returns a data frame containing Time - the year and month, and Percentage - the percent of Cahoots calls

### **Analysis**
- The first thing I noticed once I had begun analysis was the fact that there was a large number of calls with the call sign "CAHOT". These calls, however, ended up almost all containing dispositions that implied no action was taken or the call was canceled. Therefore I chose to filter out those Dispositions, and not analyze the CAHOT call sign
- I also chose to ignore the Cahoots shift 3J81 because there were only 7 calls in that set after cleaning. (This is a Springfield shift)

- The first graph in my file finds the percentage of Cahoots calls out of total calls. 
- From there I decided to do two separate graphs that show each individual shift and the percentage of calls they handle. One graph where they're stacked, and another that shows each monthly percentage individually.
- On cahoots_calls_over_time, I wanted to find counts for each month to see if a decrease in total CAD call volume or something else caused the spike in 2018.
- Plotted # of cahoots calls and total calls do give extra evidence that there is no correlation between the two values.




