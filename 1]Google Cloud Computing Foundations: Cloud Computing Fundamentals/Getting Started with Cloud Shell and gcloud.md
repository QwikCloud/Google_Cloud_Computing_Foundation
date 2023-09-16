>⚠️ PLEASE SUBSCRIBE OUR CHANNEL [QwikCloud](https://www.youtube.com/@qwikcloud)
# GSP002
## Run in cloudshell
```cmd
export PROJECT_ID=$(gcloud config get-value project)
export ZONE=$(gcloud config get-value compute/zone)

gcloud compute instances create gcelab2 --machine-type e2-medium --zone $ZONE
```
