# 4_2 : Davis® forecast analysis

We will look at how we can use Davis Predictive AI to predict the percentage of host memory usage from existing timeseries usage data.

## 1) Predictive AI : Visualize future trend in host memory usage

> Benefits for predicting : Increased visibility into future capacity demands, Improved decision making for capacity planning, Reduced costs associated with unplanned capacity increases and Increased customer satisfaction. 

- Connect to demo tenannt https://guu84124.apps.dynatrace.com/

 - Open Notebooks
 - Create new query section

!["query"](https://github.com/hakansuku/D1APACTraining/blob/main/images/DQL/querygrail.png?raw=true)

Type below query to get list of hostgroups in the tenant and run
```
fetch dt.entity.host_group
```

!["query"](https://github.com/hakansuku/D1APACTraining/blob/main/images/DQL/hostgroup.png?raw=true)

> copy the host group ID for VMWARE we will use this ID to filter our query in the next step.

> In the next section we will query the average memory usage percentage for the past 30 days grouped by hosts filtering only for the hosts that belong to VMware host group.

- Create new query section

- Type query and run query.
  
```
timeseries thisWeek = avg( dt.host.memory.usage ),
from: now()-30d,
by: {dt.entity.host},
filter: dt.entity.host_group=="HOST_GROUP-E7C1CF343BD32188"

| fields `thisWeek`, `dt.entity.host`, `interval`, `timeframe`
```

> The timeseries command is a starting command of DQL. The DQL timeseries command returns a result in the time series record format.
> It combines loading, filtering and aggregating metrics data into a time series output.

> In DQL commands are chained together using the pipe character (|). Conceptually, this is similar to Unix command pipelining, where the output of the command to the left of the pipe becomes the input of the command to the right of the pipe.

> Observe the output contains the fields thisWeek , dt.entity.host , interval and timeframe defined. 

!["line"](https://github.com/hakansuku/D1APACTraining/blob/main/images/DQL/memoryusage.png?raw=true)

- Change the visualization type by pressing OPTIONS and select Line chart

!["linechart"](https://github.com/hakansuku/D1APACTraining/blob/main/images/DQL/memorylinechart.png?raw=true)

> Next, we will now use Davis predictive AI to forecast memory percentage usage based on our timeseries dataset.

- Click Davis AI at the bottom of the chart options
- Click to enable Davis Analyzer
- Press Run Query

!["linechart"](https://github.com/hakansuku/D1APACTraining/blob/main/images/DQL/enableforecast.png?raw=true)

> Observe how easily memory usage trend is projected into the future with the help of Davis Analyzer. 

!["forecasted"](https://github.com/hakansuku/D1APACTraining/blob/main/images/DQL/forecastedmemoryusage.png?raw=true)








> Predictive AI helps teams avoid costly problems
This is just one example of predictive AI in action. But for ITOps, DevSecOps, and SRE teams, predictive AI presents numerous use cases for gaining foresight into issues and pre-emptively addressing them before they escalate into costly problems. They see improved efficiency, reduced risks of security breaches, and better compliance with industry regulations.

Similarly try forecasting disk usage percentage. (HINT: dt.host.disk.used.percent)

End of document
