# Log management environment preparation

> IMPORTANT : If you don't have SaaS (3rd Gen) with Grail tenant environment access. Please ping me and I'll give you an account.

## 1) Creating access token to ingest log records via API

> Login to your SaaS (3rd Gen) tenant environment, click search and type "Token"

Click on Access Tokens

![token](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/token.png?raw=true)

- Type a token name
- In the scope search field type log
- Tick Ingest Logs check box
- click Generate Token button

![tokennew](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/generate.png?raw=true)

> We start by generating an access token with permission scope to allow us ingest a sample log record using Dynatrace Log API

![token copy](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/newtoken.png?raw=true)

> Note: Generated token has permissions to ingest log record using API.  Click on Copy and save for later use.

## 2) Configure Dynatrace API (Swagger UI)

Open search and type "API"
Click Dynatrace API

![DTAPI](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/APIsearch.png?raw=true)

> Notice a new tab opens Dynatrace API Swagger UI interface.

Expand the dropdown and select Classic Environment API v2

![swagger](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/APIdropdown.png?raw=true)

> Swagger UI allows to visualize and interact with the API's resources without having any of the implementation logic in place.

> We will be using REST Environment API v2 functions to ingest log record. 

Click on Authorize button

![authorize](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/authorize.png?raw=true)

> We will add our new generated authentication token to be used for API request headers

Paste the generated token in step 1) into the value field and click Authorize button.

![copytoken](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/tokenauthorize.png?raw=true)

Click close to finalize adding token header.

![copytoken](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/authorizeclose.png?raw=true)

> We have now enabled Environment API v2 function requests with the authorization API-Token header.

## 3) Ingesting sample log record into Dynatrace via Log API

> Swagger UI provides friendly interface that displays Dynatrace API documentation and allows you to test Dynatrace API endpoints.

- Scroll down and expand logs section
- Expand POST /logs/ingest endpoint subsection.
- Click on Try it out button

![logs](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/logstry.png?raw=true)

- Expand drop down in Request body section and choose "text/plain, charset utf-8" 
- Copy sample log text below and paste into Examples body field (refer screenshot)

```
COR-8f69b922-038c-11ef-8aa2-72feaaeb5541 REQ-b47536b9-038c-11ef-aebe-56fa8f9f42b9 INFO core-om-com-dev-om-com-event-handler-service --- [org.springframework.kafka.KafkaListenerEndpointContainer#0-0-C-1] c.d.ps.fallout.handler.RequestUtil Fallout has been generated for this order Id 25016 and pushed to kafka {"records":[{"value":{"context":{"event":{"name":"ProductOrderInErrorEvent","timestamp":"2024-04-26T05:20:38.000362Z","eventId":"b7ac941f-038c-11ef-a28b-caaca7f9e0f9"},"producer":{"name":"COM"},"payload":{"orderInfo":{"externalKey":"6690140-2ed4-4fa7-ac01-70b8f65821b1","orderSubmittedDate":"2024-04-26T05:19:30.000833Z","orderLastUpdatedDate":"2024-04-26T05:20:38.000362Z","clientId":"TestTool","orderId":"25016","orderVersionNumber":"1","orderOperation":"CREATE","orderType":"Resume","subscriberID":"REG-926274375","customerID":"CustomerCloud2","orderStatus":"Order in Fallout","falloutInfo":{"falloutId":"8476","createdDate":"2024-04-26T05:20:33.000250Z","errorCode":"SOI-0001","failureReason":"FAILED","taskName":"acb3a7a6","workgroupName":"GlobalFallout"},"GPSI":"19525295333"}}}}}]}
```

![Tryitout](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/ingestsample.png?raw=true)

- Click Execute button

Upon Execution, you are now able to check outcome of the request looking at the responses section below.

Notice that the request headers contain authorization (API-token)

> A 204 status code is used when the server successfully processes the request, but there is no content to return to the client.

> The HTTP 200 OK success status response code indicates that the request has succeeded.

![response](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/successingest.png?raw=true)

> You have now successfully ingested a log record.  Next we will validate the log record in Dynatrace.

## 4) Validating ingested sample log record in Dynatrace
Open search and type "log"
Click to open Log & Events app

![response](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/logevents.png?raw=true)

In Log & Events page, simply click Run Query button. 

![response](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/logrecord.png?raw=true)

Observe the ingested log record and validate by looking at the timestamp and content section.

> NOTE: This method is also useful to test customer log samples.

End of Document


