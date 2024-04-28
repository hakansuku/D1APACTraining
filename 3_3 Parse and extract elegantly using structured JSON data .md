# 3_3 Parse and extract elegantly using structured JSON data 

## 1) Understanding JSON structure
- Open DPL architect from Notebooks, copy JSON data from record content.

![JSONdata](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/visualizeJSON.png?raw=true)

- copy and paste into online JSON decoder tool 

```
{"records":[{"value":{"context":{"event":{"name":"ProductOrderInErrorEvent","timestamp":"2024-04-26T05:20:38.000362Z","eventId":"b7ac941f-038c-11ef-a28b-caaca7f9e0f9"},"producer":{"name":"COM"},"payload":{"orderInfo":{"externalKey":"6690140-2ed4-4fa7-ac01-70b8f65821b1","orderSubmittedDate":"2024-04-26T05:19:30.000833Z","orderLastUpdatedDate":"2024-04-26T05:20:38.000362Z","clientId":"TestTool","orderId":"25016","orderVersionNumber":"1","orderOperation":"CREATE","orderType":"Resume","subscriberID":"REG-926274375","customerID":"CustomerCloud2","orderStatus":"Order in Fallout","falloutInfo":{"falloutId":"8476","createdDate":"2024-04-26T05:20:33.000250Z","errorCode":"SOI-0001","failureReason":"FAILED","taskName":"acb3a7a6","workgroupName":"GlobalFallout"},"GPSI":"19525295333"}}}}}]}
```

> Online JSON decoder : https://codebeautify.org/json-decode-online


