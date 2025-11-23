Travel Memory Application Deployment

Created a Backend Ubuntu Instance 


Created a Frontend Ubuntu Instance

Using the above instances, connected and updated the NodeJS and NPM application using apt install command. 
#!/bin/bash 
sudo apt update
sudo bash
sudo apt install nodejs -y
sudo apt install npm -y


Once done, cloned the git repository shared as part of the assignment.
sudo git clone https://github.com/UnpredictablePrashant/TravelMemory

Created the #nano .env to add the database MongoDB credentials.
MONGO_URI=mongodb+srv://dinxie:MongoTest@ddcluster.lcac6yg.mongodb.net/

We can access it browser by using the Public IP and port for both the front end and back end instance.

Now install the ngnix and check the status
# sudo apt install nginx
# sudo systemctl status nginx 

Now for the reverse proxy 
#sudo unlink /etc/nginx/sites-enabled/default
#cd /etc/nginx/sites-available/
#sudo nano custom_server.conf
server { 
listen 80;
location / {
proxy_pass http://my_server;
}}
#ln -s /etc/nginx/sites-available/custom_server.conf /etc/nginx/sites-enabled/custom_server.conf
#sudo service nginx configtest
#sudo service nginx restart
Creating another instances of FrontEnd and BackEnd


Using the AMIs


Creating Target Group 

2 target groups are created specifically to manage the 2 Frontend instances and 2 Backend instances.



Creating the Load Balancers and launching the web page using the same

For Backend instances:

For Frontend Instances:

