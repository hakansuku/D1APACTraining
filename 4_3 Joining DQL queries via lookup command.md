# 4_3 : Joining DQL queries via lookup command

> Very often , there are instances where you need to join data in different queries for analysis. 
> In DQL you can use the lookup command. Lookup returns a record from a subquery (the lookup table) producing a match between a field in the source table (sourceField) and a field in the lookup table (lookupField).

In the below example, we will look at how we can use lookup to compare average host disk usage week-over-week

## 1) Compare disk % usage week-over-week

> Benefits for predicting : Increased visibility into future capacity demands, Improved decision making for capacity planning, Reduced costs associated with unplanned capacity increases and Increased customer satisfaction. 

- Connect to demo tenannt https://guu84124.apps.dynatrace.com/

 - Open Notebooks
 - Create new query section

Type : 
```
timeseries thisWeek = avg( dt.host.disk.used.percent ),
from: now()-7d,
by: {dt.entity.host},
filter: dt.entity.host_group=="HOST_GROUP-E7C1CF343BD32188"

| fieldsAdd lastWeek = lookup (
[timeseries disk = avg(dt.host.disk.used.percent),
  from: now()-14d, 
  to: now()-7d,
  by: {dt.entity.host},
  filter: dt.entity.host_group=="HOST_GROUP-E7C1CF343BD32188"], 
sourceField:dt.entity.host, 
lookupField:dt.entity.host
)[disk]

| fields  dt.entity.host, diskThisWeek = arrayAvg(thisWeek), diskLastWeek = arrayAvg(lastWeek)
| fieldsAdd diff = diskThisWeek- diskLastWeek
| sort diff desc
| fieldsAdd trend = if(diff<0,"↘️", else:if(diff>=0,"↗️"))
| fieldsAdd indicator = if(diskThisWeek<95,if(diskThisWeek>50,"🟠",else:"🟢"), else:if(diskThisWeek>95,"🔴"))
```

> The first part (1) is a simple timeseries data on average disk % usage for last 7 days , we are calling it thisWeek.

> The part (2) section w use a lookup function to add a field called lastWeek of type timeseries for average disk % usage during prior week.  Note how we specify the common field dt.entity.host when joining the queries.  Please watch this 2 minutes video :link: (https://youtu.be/GeLRFpjTuPk)

> In part (3) section, we add the fields for thisWeek and lastWeek averages.  We then calculate the difference between thisWeek and lastWeek % and define indicators to display trend up and down.  Lastly we add status indicator with thresholds 🔴 > 95% > 🟠 > 50%  🟢. 


!["query"](https://github.com/hakansuku/D1APACTraining/blob/main/images/DQL/lookup.png?raw=true)

> Key takeaway : In this exercise, make sure you understand how we use lookup command to join data from two queries using a common field as a key.  And use the results for analysis. 
