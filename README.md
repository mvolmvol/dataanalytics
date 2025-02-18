<center><h2> Project <br><h1>⛈️🌪️❄️Weather vs. Flights ✈️ 🛩️ </center>

It's project time again 👷🏽‍♂️🛠️!  
In this project you will combine your Python, SQL, API and dbt skills and use them in combination with each other.  



## Objectives
As we have learned, the two main tools of Data Analysts are SQL and Python. In the last lectures and exercises, you have learned 

- how to use SQL
- retrieve data from an API and import it into a database
- transform it into insightful tables
- and get data from a database into a pandas dataframe

And now you should do it all together.




## Scenario Briefing
The Research Center for Aerospace (RCA), where you work for as Data Analyst, wants to keep track of accumulated flights data in combination with weather data. 

Your task is to find a situation where the weather conditions have impacted flight performance and provide insights on how different weather conditions affect flights in various cities / airports.

## What you need

- a weather event and the **time period** for data
- **flight data** for the time period and affected airports
- **weather data** for the time period and for the weather stations at the affected airports

![](images/PIREPs-featured.jpg)  

## Setting-up working environment

​	**Project Schema in our DB**  

1. In our DB each team will get a new project schema . Members will have write and read rights. (fingers crossed!)
2. ⚠️ **Important Note:** After a group member creates or updates a table, she or he becomes the owner of the table and needs to run a query to grant permissions to the other team members. (Coaches will provide the query to each team)

​	**Project GitHub Repo**

>This repo will be for retrieving the data from sources and loading it to the DB
>Here you can also store all your development, experiments, analysis and visualizations. Organize your repo with folders, notebooks and sql files. 
1. One team member can fork this repository to their GitHub
2. The owner then adds the team members to the repository as collaborators (in GitHub repo: **Settings** > **Collaborators** > "**Add People**" Button)
3. All team members can clone the repository from the owner to local machines
4. Check your `.gitignore` in order to avoid pushing credentials to GitHub. 

​	**dbt GitHub Repo**

>This repo will only hold the dbt project files (yml files, sql model files etc.)
1. One of you (could be same or different person) will need to create a **new empty GitHub repository for the dbt**. One owner, other team members can collaborate. 
2. Prioritize using branches and pull requests reviewed by other team members, so the `main` remains the "source of truth"
3. in dbt Cloud <u>only</u> the "dbt repo"-owner needs to ...
	#### a. modify the Schema
     <details><summary style="color:pink">(click for How-To)</summary> 
          <i>assuming you have a dbt project already</i>
          <ul>
          <li>click on your account name in the left side menu 
          <li> select <b>Your Profile</b>
          <li> in the secondary navigation select <b>Credentials</b>
          <li> click the project name and click the button in the lower right corner <b>Edit</b>
          <li> re-enter your DB passwort and change the <b>Schema</b> to your group's schema name
          <li> FYI: <b>Test Connection</b> is sometimes buggy.
          <li> click the <b>Save</b> button
          </ul>
     </details>
     
     #### b. connect to the new dbt project GitHub repository   
     
     <details><summary style="color:pink">(click for How-To)</summary> 
          <ul>
          <li>click on your account name in the left side menu 
          <li> select <b>Your Profile</b>
          <li> in the secondary navigation select <b>Project</b> and click the project name
          <li> under <b>Repository</b> click the GitHub link
          <li> click the button <b>Edit</b>
          <li> click the button <b>Disconnect</b> and then <b>Confirm Disconnect</b>
          <li> now under <b>Repository</b> click <b>Configure Repository</b>
          <li> select the <b>Git Clone</b> option (in parallel you need to go to you GitHub repo and copy the SHH git URL from your new dbt repo)
          <li> in the <b>Git URL</b> field: paste the SHH git URL and click the "Import" button
          <li> under <b>Repository</b> click the GitHub link again
          <li> copy the <b>Deploy key</b> (everything including the "ssh-rsa...")
          <li> add the <b>Deploy key</b> in your dbt repo (see <b>Settings</b>) or alternatively in your GitHub Profile Settings as <b>SSH key</b>
          </ul>
     </details><br>

⚠️**Important:** Do not mix these repositories on your local machine = Do not put one inside another. Keep them separate.

## Task Steps in Detail
1. Select a historical weather event that occurred in the United States within the past 30 years that you believe would have led to the cancellation of flights. Research online. Based on the time period when the weather event occurred, determine which timeframe for flight data would best reflect both regular traffic and the associated irregularities.  

2. Retrieve flight data as described in [fligths_data_wrangling.ipynb](fligths_data_wrangling.ipynb) and import it into the PostgreSQL database:  
     **a.** **`To Do:`** specify period  
     **b.** download and clean data `(pre-coded)`  
     **c.** **`To Do:`** Reduce your dataframe to include 3-5 origin airports (check if they have weather stations here: https://meteostat.net/en/)  
     **d.** **`To Do:`** Connect to database and import the flights data as a table in the project schema.

     **e.** From the `airports` table in schema `public` filter the relevant airports and use the result set to create a new table in your project schema. (or you copy the whole `airports` table)

3. As next step, get historical weather data using the [Meteostat API](https://dev.meteostat.net/api/point/daily.html#endpoint).   
     Based on the notebooks from our API lectures `meteostat_daily_fromAPI_toDB_lecture.ipynb`  and  `meteostat_hourly_fromAPI_toDB_lecture.ipynb` develop **new notebook(s)** to make API Calls to retrieve the necessary data, and to push it to the project schema in our database. Up to you whether you want to use API endpoints for hourly or daily weather.  
     💡**Hint:** if the period you selected for the weather event is only a few days long, go for the **hourly data**. It gives you more granularity.

4. Using **dbt Cloud** transform the original data to insightful tables which will allow you to visualize flight events and weather changes over time, to summarize useful statistics  in (e.g. to compare regular flight traffic averages with the metrics during the weather extremes)  
   💡**Hint:** actually you can use the existing yml files and all staging and prep models from our lecture. You might need to update the raw table names if you named them differently. 

5. In a Jupyter Notebook use SQLAlchemy to retrieve data from database tables and store it in pandas DataFrames. (if time is short you can also use the BBeaver's extract as CSV option)

6. With pandas you have multiple options:

     **a.** Perform a basic EDA on the initial data (prep or staging tables). The EDA should reflect what data is your project based on.  
     **b.** Come up with three different hypotheses regarding your available data. You could ask questions like 

     - "Can we see the weather event in the weather data?" 
     - "Can we see the weather event in the flights data?"
     - "Can we see a correlation between the data?"
     - "Can we see anything unusual? Any anomalies?"
     - ...

     **c.** Go deeper into your hypotheses (perhaps linking dep_delay to weather) and clearly outline your findings (either that everything is as expected or any unexpected results).  
     
     **d.** create visualizations reflecting your findings. (doesn't need to be many. Sometimes 1 or 2 charts are very insightful.)



### Deliverables
1. Jupyter notebook containing the loading and the cleaning of the flights data and the data import into the database.
2. Jupyter notebook with calls to the meteostat API and the data import into the database.
3. Jupyter notebook with EDA of weather data and flight traffic. Investigate and analyze the relationship between a specific weather event (which you’ll define) and any irregularities in flight traffic. Be sure to include relevant visualizations to support your findings.
4. ~10-minutes technical presentation (eg. via google slides) to your colleagues, presenting the results of your data exploration and answering your hypotheses.



**Keep in mind that your API calls are limited!**  
**When possible, separate code calling the API from other code working on the data.**
