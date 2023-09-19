>⚠️ PLEASE SUBSCRIBE OUR CHANNEL [QwikCloud](https://www.youtube.com/@qwikcloud)
# GSP089
## Run in cloudshell
```cmd
#Command 1
#exporting zone
export ZONE=
```
```cmd
#creating lamp-1 vm
gcloud compute instances create lamp-1-vm \
--zone=$ZONE \
--machine-type=e2-medium \
--image-project=debian-cloud \
--image-family=debian-11 \
--tags=http-server

#creating firewall rule
gcloud compute firewall-rules create allow-http \
--action=ALLOW \
--direction=INGRESS \
--rules=tcp:80 \
--source-ranges=0.0.0.0/0 \
--target-tags=http-server

#connecting ssh to cloud shell
gcloud compute ssh lamp-1-vm --zone=$ZONE
```
```cmd
#Command 2
sudo apt-get update
sudo apt-get install apache2 php7.0
sudo service apache2 restart
curl -sSO https://dl.google.com/cloudagents/add-google-cloud-ops-agent-repo.sh
sudo bash add-google-cloud-ops-agent-repo.sh --also-install
sudo apt-get update
```
## Now perform the 3rd and 4th task manually