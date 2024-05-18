# README.md

## data_cleaning_final.ipynb

### Libraries
- pandas

### Cleaning Steps Taken
  - Import call data from CAD
  - Change Call_Created_Time to pd.datetime form
  - Rename "Call_Created_Time" to "Call Time"
  - Selected relevant columns for my analysis ["Call Time", "PrimaryUnitCallSign", "RespondingUnitCallSign", "InitialIncidentTypeDescription", "Disposition"]
  - Removed rows with "InitialIncidentTypeDescription" are empty, I need that rows with that info for further analysis
  - Removed rows where both "PrimaryUnitCallSign" and "RespondingUnitCallSign" are empty
  - Renamed columns as follows to increase ease of analysis for me {"PrimaryUnitCallSign": "Call Sign", "InitialIncidentTypeDescription": "Reason for Dispatch", "RespondingUnitCallSign": "2 Call Sign"}
  - Set the file to automatically save to the current folder after cleaning for easy transfer to next file.

## cahoots_calls_over_time.ipynb
### Libraries
  - pandas, matplotlib.pyplot, and datetime libraries necessary
### Helper Functions:
- cahoots_call_signs:
  - A list of the cahoots call signs in Eugene that I will be analyzing in this project.

- time_filter_year:
  - A helper function to quickly filter dataframes by year. Used in later analysis

- time_filter_month:
  - Another helper function used to filter times monthly given a start and end month and year.
  percent_cahoots_calls:
  - Calculates the percentage of calls where either call sign or 2 call sign contains a cahoots call sign out of the total calls

- filter_incidents:
  - Takes a dataframe, column name, and list
  - returns a dataframe where the columns incidents are contained in the list

- calc_monthly_percentages:
  - Given a dataframe and a list of cahoots call signs, it returns the percentage of cahoots calls out of total calls by month
  - Returns a dataframe containing Time - the year and month, and Percentage - the percent of Cahoots calls

- 

### **Analysis**
#### **What I did**
- Plotted Monthly Percent of Cahoots Calls out of total CAD calls. Labeled first occurrence of each new call sign
- Plotted each individual call percent as part of the whole
- Plotted each individual percent out of the total cahoots calls
- Computed the average percentage of calls handled for each call sign in each given time period
- Found the count of each cahoots call sign per month and plotted those against the total CAD calls
- Zoomed in on previous graph to show total count of Cad calls and calls per sign
- Made a scatter plot for Cahoots calls vs total calls differentiated by time period to show correlation between added capacity and call volume

#### **Observations**
- The first thing I noticed once I had begun analysis was the fact that there was a large number of calls with the call sign "CAHOT". These calls however, ended up almost all containing dispositions that implied no action was taken or the call was canceled. Therefore I chose to filter out those Dispositions, and not analyze the CAHOT call sign
- I also chose to ignore the Cahoots shift 3J81 because there were only 7 calls in that set after cleaning. (This is a Springfield shift)

- The first graph in my file finds the percentage of Cahoots calls out of total calls. 
- From there I decided to do two seperate graphs that show each individual shift and the percentage of calls they handle. One graph where they're stacked, and another that shows each monthly percentage individually.
- Lastly on cahoots_calls_over_time I wanted to find counts for each month to see if there was a decrease in total CAD call volume or somthing else that caused the spike in 2018.
- Considering a Chi-Squared test, not quite sure how to implement yet. More reading is necissary.




