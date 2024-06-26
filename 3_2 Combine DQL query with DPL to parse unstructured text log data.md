# Combine DQL query with DPL to parse unstructured text log data

> Dynatrace Pattern Language (DPL) is a pattern language that allows you to describe patterns using matchers, where a matcher is a mini-pattern that matches a certain type of data

>Use DPL to:
Parse a record field into multiple output fields with the DQL parse command.
Reshape incoming data for better understanding, analysis, or further processing, in Log and event processing.

## 1) Rapidly develop DPL expressions using DPL Architect and extract fields from log record

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
> How DPL works : Imagine a location pointer is moving from the start to the end of the record data.

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/DPLAinitialscreen.png?raw=true)

> DATA is an DPL expression that matches anything.  Similar to a wildcard (*) Matches any number of characters. .
> Hence notice the whole content is highlighted.  It is matching any characters as the pointer moves from the start to the end of the record.

> If we add a specific expression to match next to DATA.  For example DATA 'name'.  The pointer will go from start matching anything up to the first occurrence of the word name.

- Type DATA 'name'
  
![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/namematch.png?raw=true)

> observe how the matching is highlighted up to the first occurrence of the word name. The pointer location is at the end of word name.

- Type DATA 'name' DATA (this would be similar to wildcard * name *)
  
![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/datanamedata.png?raw=true)

> observe the highlighted area.  The pointer starts from start where first DATA expression matches anything up to the first occurrence of the word name then again second expression DATA matches anything to the end. The location of the pointer is end of the record.

- Type
```
DATA 'name' DATA 'orderId'
```

> Notice that I enclose the specific matching word expression within single quotes ' '.
Again observe the matched areas highlighted. the last location of the pointer is at the end of word orderId.

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/datanamedataorderId.png?raw=true)

> Grasping this concept is extremely important as we can then pin-point the pointer at the exact position where to start and end to extract a value from the record. 

> To extract data at a pointer location we add syntax as
### :\<variable name\>      
> for example  :myname 

Now lets extract the orderId value. 

- Type 
```
DATA 'orderId":"' DATA:myorderId '"'
```

>Note second DATA expression starts from character after 'orderId":"' and finishes before '"'.  You need to specify an end point so that second DATA expression exactly contains the wanted portion which is then passed to myorderId.

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/orderIdextract.png?raw=true)

Click Results tab to view the extracted myorderId value

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/resultorderId.png?raw=true)

> Notice how easy it is to build and check the result of pattern expressions with DQL Architect.

With the above learning, try to extract another value for example eventId value b7ac941f-038c-11ef-a28b-caaca7f9e0f9

## 2) Extracting multiple values 

> In this example using the same concept as in step 1) , we will extract 4 values ( event_name ,  event_timestamp, event_Id, orderId

Type 
```
data 'name":"' data:event_name '","timestamp":"' data:event_timestamp '","eventId":"' data:event_Id '"' data 'orderId":"' data:orderId '"'
```
> I have underlined with colour lines. Try to observe how each expressions match so you can follow the pointer positions that dermine the extraction locations.

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/multivalues.png?raw=true)

Click on results tab to validate the extracted values (simply expand the sections if you can read or hover your cursor over the value and it will pop up)

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/cursorhoverpopup.png?raw=true)

> You can also arrange the syntax in multiple lines, whichever way is more readable to your comfort.

```
data 'name":"' 
data:event_name '","timestamp":"' 
data:event_timestamp '","eventId":"' 
data:event_Id '"' 
data 'orderId":"' data:orderId '"'
```

> Notice that using DATA as the matcher always stores the data format to STRING.  You can easily format the data during extraction by replacing with the corresponding data type.

From the record text we can recognize the timestamp format follows JSONTIMESTAMP data type format and orderId is numeric so can be stored as INTEGER data type format. 
Replace the expression with 

```
data 'name":"' 
data:event_name '","timestamp":"' 
JSONTIMESTAMP('yyyy-MM-ddTHH:mm:ss.SSSSSSZ'):event_timestamp '","eventId":"' 
data:event_Id '"' 
data 'orderId":"' INT:orderId '"'
```

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/dataformatconversion.png?raw=true)
> Notice how the data format has now changed for event_timestamp and orderId.

## 3) Applying DPL expressions to log processing rules.
- Open log & events application
- Switch to advanced mode
- Run query

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/openlogadvancedmode.png?raw=true)

> Observe that there are only 6 fields in the record we ingested. (timestamp, status, content, loglevel, event.type, dt.auth.origin)

- click on the log record
- click on create processing rule

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/createprocessingrule.png?raw=true)

- Type in the Rule name field
- Type isNotNull(`dt.auth.origin`) in the matcher field
- Type in processor definition
  
```
parse(content , "
data 'name\":\"' 
data:event_name '\",\"timestamp\":\"' 
JSONTIMESTAMP('yyyy-MM-ddTHH:mm:ss.SSSSSSZ'):event_timestamp '\",\"eventId\":\"' 
data:event_Id '\"' 
data 'orderId\":\"' INT:orderId '\"'
")
```
> NOTE as DPL is wrapped inside parse, quotation mark inside a quotated string requires protecting it with a backslash. 

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/parcingruleMK.png?raw=true)

scroll down and click on run rule test

![dplarchitect](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/runruletest.png?raw=true)

> Observe how 4 fields are now extracted from content as attributes in the test result.

Click Save Changes

> We will now test by ingesting the same record again 
Refer course 3_1 step 3) to ingest log record using Log API using SWAGGER UI

- Ingest same sample record again using Dynatrace Log API Swagger UI
- Click Run Query

![processing rule](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/4fieldextractionrunqueryresult.png?raw=true)

> Observe the 4 fields available as attributes.  You can also validate the record fields with fetch logs from Notebooks app.

End of Document


