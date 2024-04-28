# 3_2 - Combine DQL query with DPL to parse simple text field

> Dynatrace Pattern Language (DPL) is a pattern language that allows you to describe patterns using matchers, where a matcher is a mini-pattern that matches a certain type of data

>Use DPL to:
Parse a record field into multiple output fields with the DQL parse command.
Reshape incoming data for better understanding, analysis, or further processing, in Log and event processing.

## 1) Rapidly develop DPL expressions using DPL Architect and extract fields from log records

> DPL Architect provides instant feedback to your DPL pattern expression without the need to re-execute your DQL query. This saves you time and energy when determining what DPL expression you need. Feedback is given in two contexts: base dataset and match preview dataset.

- Open search and type "Notebook"
- Click on Notebooks 

![notebook](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/notebook.png?raw=true)

> To open DPL Architect
- Click new query
- Choose Logs and click on Fetch logs

![fetchlog](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/fetchlogs.png?raw=true)

- In the query section, select Run query.
- In the results section, observe our ingested log record.  Select the content cell and then select Extract fields from the pop-up menu.

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/dplarchitect.png?raw=true)
> How DPL works : Imagine reading from the start to the end of the record data.

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/DPLAinitialscreen.png?raw=true)

> DATA is an DPL expression that matches anything.  Similar to a wildcard (*) Matches any number of characters. .
> Hence notice the whole content string is highlighted.  It is matching any characters from the start to the end of the record.

> If we add a specific expression to match next to DATA.  For example DATA 'name'.  It will go from start matching anything up to the first occurrence of the string name.

- Type DATA 'name'
  
![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/namematch.png?raw=true)

