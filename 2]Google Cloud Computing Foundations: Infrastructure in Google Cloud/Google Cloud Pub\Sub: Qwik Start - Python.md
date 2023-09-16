# GSP094
>⚠️ PLEASE SUBSCRIBE OUR CHANNEL [QwikCloud](https://www.youtube.com/@qwikcloud)
## Run in cloudshell
```cmd
#Creating a virtual environment
sudo apt-get install -y virtualenv
python3 -m venv venv

#Activiating the environment
source venv/bin/activate

#Installing the client library
pip install --upgrade google-cloud-pubsub
git clone https://github.com/googleapis/python-pubsub.git
cd python-pubsub/samples/snippets

#Creating a Topic
python publisher.py $GOOGLE_CLOUD_PROJECT create MyTopic

#Creating a Subscription
python subscriber.py $GOOGLE_CLOUD_PROJECT create MyTopic MySub
```