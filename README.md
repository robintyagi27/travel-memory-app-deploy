# Travel Memory Application Deployment

# Created a Backend Ubuntu Instance 

<img width="1551" height="610" alt="image" src="https://github.com/user-attachments/assets/d8d34e21-ff1c-4807-aeff-a98ec5070440" />

# Created a Frontend Ubuntu Instance

<img width="1568" height="588" alt="image" src="https://github.com/user-attachments/assets/19def8ae-146e-4a2e-8e7e-ef396aec4963" />

# Using the above instances, connected and updated the NodeJS and NPM application using apt install command. 
#!/bin/bash 
sudo apt update
sudo bash
sudo apt install nodejs -y
sudo apt install npm -y


# Once done, cloned the git repository shared as part of the assignment.

sudo git clone https://github.com/UnpredictablePrashant/TravelMemory

# Created the #nano .env to add the database MongoDB credentials.

MONGO_URI=mongodb+srv://dinxie:MongoTest@ddcluster.lcac6yg.mongodb.net/

We can access it browser by using the Public IP and port for both the front end and back end instance.

# Now install the ngnix and check the status

sudo apt install nginx
sudo systemctl status nginx 

# Now for the reverse proxy 

sudo unlink /etc/nginx/sites-enabled/default
cd /etc/nginx/sites-available/
sudo nano custom_server.conf
server { 
listen 80;
location / {
proxy_pass http://my_server;
}}
ln -s /etc/nginx/sites-available/custom_server.conf /etc/nginx/sites-enabled/custom_server.conf
sudo service nginx configtest
sudo service nginx restart

# Creating another instances of FrontEnd and BackEnd
<img width="1566" height="610" alt="image" src="https://github.com/user-attachments/assets/b8dee90d-d2b3-4069-a201-c8281361c8da" />

<img width="1567" height="614" alt="image" src="https://github.com/user-attachments/assets/ef334a88-493e-4076-a7b0-7bf89ce67538" />

# Using the AMIs

<img width="1607" height="182" alt="image" src="https://github.com/user-attachments/assets/8840e925-8fac-40d6-8398-c37232d79a85" />

# Creating Target Group 

<img width="1596" height="194" alt="image" src="https://github.com/user-attachments/assets/417f48f3-3ea5-4962-aaf3-ea7959ec9f8e" />


# 2 target groups are created specifically to manage the 2 Frontend instances and 2 Backend instances.

<img width="1555" height="783" alt="image" src="https://github.com/user-attachments/assets/af898c3a-4965-48d0-bee1-9e8e881a551c" />

<img width="1569" height="784" alt="image" src="https://github.com/user-attachments/assets/da730619-6a45-4845-b99a-3252bd3f5236" />

# Creating the Load Balancers and launching the web page using the same

# For Backend instances:

<img width="1886" height="961" alt="image" src="https://github.com/user-attachments/assets/09ff3147-0341-4cba-93d3-a23c664adbdc" />

# For Frontend Instances:

<img width="1851" height="969" alt="image" src="https://github.com/user-attachments/assets/f21e5649-48af-4789-8398-25b8bb551a20" />


