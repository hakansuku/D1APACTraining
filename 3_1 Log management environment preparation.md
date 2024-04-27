# 3_1 - Log management environment preparation

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

## 1) Ingesting sample log record using Dynatrace API (Swagger UI)

Click search and type "API"
Click Dynatrace API

![DTAPI](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/APIsearch.png?raw=true)

> Notice a new tab opens Dynatrace API Swagger UI interface.

Expand the dropdown and select Classic Environment API v2

![swagger](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/APIdropdown.png?raw=true)

> Swagger UI allows to visualize and interact with the API's resources without having any of the implementation logic in place.
> We will be using Environment API v2 to ingest a log record

![env api](https://github.com/hakansuku/D1APACTraining/blob/main/images/DPL/authorize.png?raw=true)


