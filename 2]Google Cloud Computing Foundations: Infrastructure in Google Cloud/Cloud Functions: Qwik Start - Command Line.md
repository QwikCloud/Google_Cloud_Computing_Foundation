>⚠️ PLEASE SUBSCRIBE OUR CHANNEL [QwikCloud](https://www.youtube.com/@qwikcloud)
# GSP080
## Run in cloudshell
```cmd
#Export the region variable
export REGION=

#Set the default region
gcloud config set compute/region $REGION

#Create a directory
mkdir gcf_hello_world
cd gcf_hello_world

#Creating index file
cat > index.js << EOF
exports.helloWorld = (data, context) => {
const pubSubMessage = data;
const name = pubSubMessage.data
    ? Buffer.from(pubSubMessage.data, 'base64').toString() : "Hello World";
console.log("My Cloud Function: "+name);
};
EOF

#Creating a bucket
gsutil mb -p $DEVSHELL_PROJECT_ID gs://$DEVSHELL_PROJECT_ID

#Deploy the function
gcloud functions deploy helloWorld \
--stage-bucket $DEVSHELL_PROJECT_ID \
--trigger-topic hello_world \
--runtime nodejs20
```
