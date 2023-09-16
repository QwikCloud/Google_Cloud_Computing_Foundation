# GSP164
>⚠️ PLEASE SUBSCRIBE OUR CHANNEL [QwikCloud](https://www.youtube.com/@qwikcloud)
## Run in cloudshell
```cmd
#Getting sample code
gsutil cp gs://spls/gsp164/endpoints-quickstart.zip .

#Deplying the endpoints
unzip endpoints-quickstart.zip
cd endpoints-quickstart/scripts
./deploy_api.sh

#Deploying the API backend
./deploy_app.sh

#Sending request to the API
./query_api.sh
./query_api.sh JFK
./deploy_api.sh ../openapi_with_ratelimit.yaml

#Deploying API backend
./deploy_app.sh
gcloud alpha services api-keys create --display-name="QwikCloud" 
KEY_NAME=$(gcloud alpha services api-keys list --format="value(name)" --filter "displayName=QwikCloud")
export API_KEY=$(gcloud alpha services api-keys get-key-string $KEY_NAME --format="value(keyString)")

#Tracking API activity
./query_api_with_key.sh $API_KEY
./generate_traffic_with_key.sh $API_KEY
./query_api_with_key.sh $API_KEY
```