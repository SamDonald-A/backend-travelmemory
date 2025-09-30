**Deploying MERN Application on AWS**

Useful Links:

GitHub -
[[https://github.com/SamDonald-A/TravelMemory]{.underline}](https://github.com/SamDonald-A/TravelMemory)

Frontend -
<https://github.com/SamDonald-A/Frontend-TravelMemory/tree/master>

Backend -
<https://github.com/SamDonald-A/backend-travelmemory/tree/master>

<img width="796" height="1030" alt="image" src="https://github.com/user-attachments/assets/2b207dc5-c331-4904-834b-32129e9e5a5c" />


**Backend Configuration**

**Step 1: Creating a new backend instance and connecting to it via SSH
using the instance\'s DNS address.**

<img width="975" height="519" alt="image" src="https://github.com/user-attachments/assets/a544fc05-ed32-4e56-84da-58a35747cff3" />


**Step 2: Installing GitHub in backend Instance**

*Command for Installing Git:*

sudo yum install git

*Expected Output:*

<img width="975" height="119" alt="image" src="https://github.com/user-attachments/assets/c646a74b-2622-4ccf-be15-d8382926dbbe" />


**Step 3: Go to the Travel Memory app and fork the link to copy the
repository to my github account**

<img width="982" height="503" alt="image" src="https://github.com/user-attachments/assets/f4db8684-a397-478f-88fd-c9e3c7217198" />


**Step 4: Copy the link from GitHub and clone it in the backend
Instance**

<img width="630" height="532" alt="image" src="https://github.com/user-attachments/assets/cde434f3-8b78-42ad-885b-ede2e2292558" />


*Command for Git Clone: Kindly replace the link with your link*

git clone https://github.com/SamDonald-A/TravelMemory.git

*Expected Output:*

<img width="975" height="281" alt="image" src="https://github.com/user-attachments/assets/533c61c5-621b-4838-99ce-e6c6b964a035" />


*Command to see files:*

\# See the cloned files in the present directory\
ls

\# Go in to the backend folder\
cd backend

*Expected Output:*

<img width="975" height="81" alt="image" src="https://github.com/user-attachments/assets/4f6e33e6-e580-40eb-87b6-eb7195bc08c8" />


**Step 5: Setup MongoDB and get the connection string**

<img width="837" height="400" alt="image" src="https://github.com/user-attachments/assets/5d369851-9cfe-4ca3-87ba-d62942c31c46" />


**Step 6: In the backend create ".env" and past the connection string in
the MONGO_URI variable, and PORT.**

\# To create .env file and edit the file\
sudo nano .env

\# After adding the URI and PORT check once again\
cat .env

*Expected Output:*

<img width="837" height="400" alt="image" src="https://github.com/user-attachments/assets/2eb8afc7-f71f-40d8-b07e-5e92f283f589" />


**Step 6: Install Nodejs in the backend.**

\# To create .env file and edit the file\
sudo yum install -y nodejs

*Expected Output:*

<img width="976" height="356" alt="image" src="https://github.com/user-attachments/assets/dfe75086-5148-4dac-a9dc-b8c43a3d46d4" />


**Step 7: Install npm for your backend node modules.**

npm install

*Expected Output:*

<img width="975" height="394" alt="image" src="https://github.com/user-attachments/assets/5d17b74b-751a-41e2-8031-7703fba669b9" />


**Step 8: Install nginx and configure nginx server in backend.**

\# To install nginx\
sudo yum install nginx

\# To config nginx

sudo nano /etc/nginx/conf.d

\# Create backend config

sudo nano backend.conf

*Expected Output:*

\# After configure the nginx\
server {

listen 80;

server_name your-backend-domain.com;

location / {

proxy_pass http://127.0.0.1:3000;

proxy_http_version 1.1;

proxy_set_header Upgrade \$http_upgrade;

proxy_set_header Connection \'upgrade\';

proxy_set_header Host \$host;

proxy_cache_bypass \$http_upgrade;

}

}

**Step 9: Start Nginx and Run backend.**

\# To start backend\
sudo systemctl start nginx

\# To start backend\
node index.js

*Expected Output:*

<img width="975" height="69" alt="image" src="https://github.com/user-attachments/assets/00e4344d-bdd8-455e-9326-f6ee6f8d4b48" />


**Step 10: Check backend on browser, Since Nginx enabled, No need to add
:3000 in URL**

*Expected Output:*

  -----------------------------------------------------------------------------------------------
  ![](vertopal_149c15049fa547f18a5e371c1d8db7cb/media/image13.jpeg){width="6.269564741907262in"
  height="2.5194444444444444in"}
  -----------------------------------------------------------------------------------------------

  -----------------------------------------------------------------------------------------------

**Step 10: Stop the instance and create AMI -- Amazon Machine Image from
EC2 console**

-   In EC2 Console on the left menu under images we see option for AMI's

-   Go into the option AMI and create Image using the backend Instance

<img width="940" height="378" alt="image" src="https://github.com/user-attachments/assets/8d463ce8-5938-4f31-95c8-4a17fbb3a939" />


**Step 11: Create Two EC2 Instances using AMI -- These two for scaling &
Load distribution**

-   Select right AMI in the Application and OS Images section while
    creating Instances

<img width="975" height="493" alt="image" src="https://github.com/user-attachments/assets/a370f227-de3d-47a8-853d-d305a442ff8b" />


-   Two Instances Created using same backend Image

<img width="976" height="48" alt="image" src="https://github.com/user-attachments/assets/4c27c324-b969-449f-9ea4-363d80203332" />


**Step 12: Create target group for Load Balancer**

-   Go to Target Groups under Load Balancer in EC2 left menu

-   Create target group by selecting two new backend Instances

-   Keep the HTTP and Port 80 options under protocol option and create
    Target group

<img width="975" height="283" alt="image" src="https://github.com/user-attachments/assets/4d6c9640-95da-4175-83f8-8b5facb48e84" />

**Step 13: Create Load Balancer**

-   Go to Load Balancer under Load Balancer in EC2 left menu and create
    load balancer

-   Select Application Load balancer and select backend target group
    that was created

<img width="687" height="533" alt="image" src="https://github.com/user-attachments/assets/b362bf63-35c1-4f8e-ae7b-4e45cbbbbbb1" />


-   After creating the load balancer, we get the ALB DNS name which is
    the backend URL

<img width="975" height="482" alt="image" src="https://github.com/user-attachments/assets/b1deb115-5f10-490e-b962-dc3faf3b5930" />


-   Pass this URL in browser and check if it's able to connect with
    database and retrieve data from MongoDB using /trip end point

<img width="976" height="500" alt="image" src="https://github.com/user-attachments/assets/f758390e-4797-4cbd-ac1c-a869220c6017" />


So far, the Backend Part is created successfully

<img width="700" height="949" alt="image" src="https://github.com/user-attachments/assets/e3cc0699-830b-4020-b7ff-c0beda78cb0b" />


The same way we are going to create the Frontend with few small changes.
