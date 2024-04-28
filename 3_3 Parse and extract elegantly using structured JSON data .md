# 3_3 Parse and extract elegantly using structured JSON data 

## 1) Understanding JSON structure with visualization
- Open DPL architect from Notebooks, copy JSON data from record content.

![JSONdata](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/visualizeJSON.png?raw=true)

- copy and paste into online JSON decoder tool 

```
{"records":[{"value":{"context":{"event":{"name":"ProductOrderInErrorEvent","timestamp":"2024-04-26T05:20:38.000362Z","eventId":"b7ac941f-038c-11ef-a28b-caaca7f9e0f9"},"producer":{"name":"COM"},"payload":{"orderInfo":{"externalKey":"6690140-2ed4-4fa7-ac01-70b8f65821b1","orderSubmittedDate":"2024-04-26T05:19:30.000833Z","orderLastUpdatedDate":"2024-04-26T05:20:38.000362Z","clientId":"TestTool","orderId":"25016","orderVersionNumber":"1","orderOperation":"CREATE","orderType":"Resume","subscriberID":"REG-926274375","customerID":"CustomerCloud2","orderStatus":"Order in Fallout","falloutInfo":{"falloutId":"8476","createdDate":"2024-04-26T05:20:33.000250Z","errorCode":"SOI-0001","failureReason":"FAILED","taskName":"acb3a7a6","workgroupName":"GlobalFallout"},"GPSI":"19525295333"}}}}}]}
```

> Online JSON decoder : https://codebeautify.org/json-decode-online

![JSONdata](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/visualJSON.png?raw=true)

> Expand the JSON object structure to visualize the nexted fields.

## 2) Build DPL expression for structured JSON data

- Open DPL Architect and type :
```
DATA 'pushed to kafka ' JSON:parsedJson EOL 
```

![JSONdata](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/JSONvariantobject.png?raw=true)

- Click on results tab

![JSONdata](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/resultvariantobject.png?raw=true)

> Observe the JSON data format is VARIANT OBJECT. You don't have to list all of the attributes. Instead, a JSON matcher can be used in auto-discovery mode. As a result, you get a VARIANT_OBJECT that you can process further.

- Open Log & Events app and click Run Query.
- In advanced mode, select the ingested sample record and click on Create processing rule button 

![JSONdata](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/JSONmkrule.png?raw=true)

- Type in the Rule name field
- Type isNotNull(dt.auth.origin) in the matcher field
- Type in process definition

```
PARSE(content, "DATA 'pushed to kafka ' JSON:parsedJson EOL ")
| FIELDS_ADD(event.name: parsedJson[records][0][value][context][event][name])
| FIELDS_ADD(event.timestamp: parsedJson[records][0][value][context][event][timestamp])
| FIELDS_ADD(event.eventId: parsedJson[records][0][value][context][event][eventId])
| FIELDS_ADD(producer.name: parsedJson[records][0][value][context][producer][name])
| FIELDS_ADD(orderInfo.externalKey: parsedJson[records][0][value][context][payload][orderInfo][externalKey])
| FIELDS_ADD(orderInfo.orderSubmittedDate: parsedJson[records][0][value][context][payload][orderInfo][orderSubmittedDate])
| FIELDS_ADD(orderInfo.orderLastUpdatedDate: parsedJson[records][0][value][context][payload][orderInfo][orderLastUpdatedDate])
| FIELDS_ADD(orderInfo.clientId: parsedJson[records][0][value][context][payload][orderInfo][clientId])
| FIELDS_ADD(orderInfo.orderId: parsedJson[records][0][value][context][payload][orderInfo][orderId])
| FIELDS_ADD(orderInfo.orderVersionNumber: parsedJson[records][0][value][context][payload][orderInfo][orderVersionNumber])
| FIELDS_ADD(orderInfo.orderOperation: parsedJson[records][0][value][context][payload][orderInfo][orderOperation])
| FIELDS_ADD(orderInfo.orderType: parsedJson[records][0][value][context][payload][orderInfo][orderType])
| FIELDS_ADD(orderInfo.subscriberID: parsedJson[records][0][value][context][payload][orderInfo][subscriberID])
| FIELDS_ADD(orderInfo.customerID: parsedJson[records][0][value][context][payload][orderInfo][customerID])
| FIELDS_ADD(orderInfo.orderStatus: parsedJson[records][0][value][context][payload][orderInfo][orderStatus])
| FIELDS_ADD(falloutInfo.falloutId: parsedJson[records][0][value][context][payload][orderInfo][falloutInfo][falloutId])
| FIELDS_ADD(falloutInfo.createdDate: parsedJson[records][0][value][context][payload][orderInfo][falloutInfo][createdDate])
| FIELDS_ADD(falloutInfo.failureReason: parsedJson[records][0][value][context][payload][orderInfo][falloutInfo][failureReason])
| FIELDS_ADD(falloutInfo.createdDate: parsedJson[records][0][value][context][payload][orderInfo][falloutInfo][createdDate])
| FIELDS_ADD(falloutInfo.taskName: parsedJson[records][0][value][context][payload][orderInfo][falloutInfo][taskName])
| FIELDS_ADD(GPSI: parsedJson[records][0][value][context][payload][orderInfo][GPSI])
| FIELDS_REMOVE(parsedJson)
```
- scroll down and click run test rule button
  
![JSONdata](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/JSONtestrun123.png?raw=true)

- Click Save changes button.
- Disable previous 3_2 unstructured text processing rule created.

> We will now test by ingesting the same record again. Refer course 3_1 step 3) to ingest log record using Log API using SWAGGER UI

- Ingest same sample record again using Dynatrace Log API Swagger UI
- Validate that all the JSON structure fields are added as attributes in the new ingested log record.

End of Document



