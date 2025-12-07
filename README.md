# TravelMemory MERN Stack Deployment on AWS
 
# Project Overview

This project demonstrates end-to-end deployment of a full MERN Stack application on AWS EC2 using scalable architecture, system monitoring, reverse proxying, load balancing, and domain/DNS setup via Cloudflare.

# The objective was to:

Deploy backend and frontend services.

Enable scalable multi-instance hosting.

Configure automated traffic distribution using AWS Application Load Balancers.

Connect a custom domain using Cloudflare DNS.

# Tech Stack

Frontend: React

Backend: Node.js + Express

Database: MongoDB (local EC2 installation)

Reverse Proxy: NGINX

Process Manager: PM2

Cloud: AWS EC2

Load Balancer: AWS Application Load Balancer (ALB)

DNS: Cloudflare

Domain: robin27.in

# Final Architecture

Users
   |
Cloudflare DNS
   |
--------------------------
|                        |
app.robin27.in           api.robin27.in
Frontend ALB             Backend ALB
|                        |
FE-1       FE-2          BE-1        BE-2
                           |
                        MongoDB

# Deployment Steps

# 1️ Backend Setup

On two EC2 instances:

sudo apt install nginx nodejs mongodb -y
git clone https://github.com/UnpredictablePrashant/TravelMemory.git
cd TravelMemory/backend
npm install


Create .env:

MONGO_URI=mongodb://127.0.0.1:27017/travelmemory
PORT=3001


Run with PM2:

pm2 start index.js
pm2 save


NGINX reverse proxy:

server {
    listen 80;
    location / {
        proxy_pass http://localhost:3001;
    }
}

# 2️ Frontend Setup

On two EC2 instances:

git clone https://github.com/UnpredictablePrashant/TravelMemory.git
cd TravelMemory/frontend
npm install


Create .env:

REACT_APP_BACKEND_URL=http://api.robin27.in


Build app:

npm run build
sudo cp -r build/* /var/www/travelmemory-frontend


NGINX static serving:

server {
    listen 80;
    root /var/www/travelmemory-frontend;
}

# 3️ AWS Load Balancing
Backend Target Group

2 backend EC2 instances (port 80)

Backend ALB

Forwards traffic to backend target group.

Frontend Target Group

2 frontend EC2 instances (port 80)

Frontend ALB

Serves React frontend.

# 4️ Cloudflare DNS Setup
Type	Subdomain	Target
CNAME	api.robin27.in	Backend ALB DNS
CNAME	app.robin27.in	Frontend ALB DNS

# Final Working URLs

Service	URL
Frontend UI	http://app.robin27.in

Backend API	http://api.robin27.in

# Screenshots

# Backend ALB
<img width="1314" height="733" alt="image" src="https://github.com/user-attachments/assets/71f4f3c6-fcc6-41f8-98e5-038db38131f7" />

# Frontend ALB
<img width="1643" height="807" alt="image" src="https://github.com/user-attachments/assets/863180f7-37ac-43b0-9190-4d778f97ab97" />

# Healthy target groups
<img width="1647" height="541" alt="image" src="https://github.com/user-attachments/assets/f26c23fa-af22-49da-ae39-28eec7d01451" />
<img width="1652" height="820" alt="image" src="https://github.com/user-attachments/assets/246b8abc-8b41-4929-8ae6-40073306b757" />

# PM2 running backends
<img width="1113" height="196" alt="image" src="https://github.com/user-attachments/assets/db974338-3cb5-4705-9f27-25a019f8fb72" />

# nginx status
<img width="1149" height="324" alt="image" src="https://github.com/user-attachments/assets/9aa2aebe-ed84-4644-8c6e-0ddd18db010d" />

# Cloudflare DNS records
<img width="1727" height="644" alt="image" src="https://github.com/user-attachments/assets/c0304bcf-8c1f-44b3-b6ac-6378a6543a5f" />

# app.robin27.in UI loaded
<img width="405" height="136" alt="image" src="https://github.com/user-attachments/assets/a52b4fc2-fb9c-4245-8aad-0a92723e292d" />

# api.robin27.in backend reachable
<img width="391" height="136" alt="image" src="https://github.com/user-attachments/assets/cf95f517-dbc3-431d-8b55-839c6a9262b3" />

