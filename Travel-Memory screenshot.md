**Travel Memory Application Deployment**

**Task1🡪 Backend and Frontend Configuration**

Create two EC2 instances initially for Travel Memory application deployment.

![](./Travel-Memory%20screenshot_images/image-001.png)

![](./Travel-Memory%20screenshot_images/image-002.png)

![](./Travel-Memory%20screenshot_images/image-003.png)

Redirect to instances to see the EC2 instances that we have launched recently.

Below are instances which we have created.

-   Travel-Memory-Frontend-1
-   Travel-Memory-Backend-1

![](./Travel-Memory%20screenshot_images/image-004.png)

**Backend Setup**

Login to the backend instance (Travel-Memory-Backend-1) using ssh from PowerShell

![](./Travel-Memory%20screenshot_images/image-005.png)

Switch to Root user and update the repository

-   apt update -y

![](./Travel-Memory%20screenshot_images/image-006.png)

Install packages:

-   apt install nginx nodejs npm git -y

![](./Travel-Memory%20screenshot_images/image-007.png)

Run below commands to check all the dependencies are successfully installed.

![](./Travel-Memory%20screenshot_images/image-008.png)

Clone the TravelMemory repository backend code from GitHub and redirect to the backend folder to see all the content inside backend folder of TravelMemory application repository.

![](./Travel-Memory%20screenshot_images/image-009.png)

![](./Travel-Memory%20screenshot_images/image-010.png)

**Install required dependencies in the Backend:**

-   npm install

![](./Travel-Memory%20screenshot_images/image-011.png)

Create .env file

-   nano .env

paste below properties

PORT=3001

MONGO\_URI=mongodb+srv://handyguy495\_db\_user:<**db\_password**\>@clusternew5.o35be6r.mongodb.net/?appName=ClusterNew5

![](./Travel-Memory%20screenshot_images/image-012.png)

Once above .env file is created then install pm2 process manager to start the backend and to keeps backend application running in the background.

-   npm install -g pm2

Then start the backend using below command.

-   pm2 start index.js --name backend

![](./Travel-Memory%20screenshot_images/image-013.png)

Please save pm2 by running this command

-   pm2 save

![](./Travel-Memory%20screenshot_images/image-014.png)

Please test backend whether the backend code running properly:

![](./Travel-Memory%20screenshot_images/image-015.png)

**Frontend Setup**

Login to the Frontend instance (Travel-Memory-Frontend-1) using ssh from PowerShell

![](./Travel-Memory%20screenshot_images/image-016.png)

Switch to Root user and update the repository

-   apt update -y

![](./Travel-Memory%20screenshot_images/image-017.png)

**Install packages:**

-   apt install git nginx nodejs npm -y

![](./Travel-Memory%20screenshot_images/image-018.png)

![](./Travel-Memory%20screenshot_images/image-019.png)

![](./Travel-Memory%20screenshot_images/image-020.png)

Now installing dependencies

npm install

![](./Travel-Memory%20screenshot_images/image-021.png)

Now we have to create .env file for Frontend whare we have to give backend URI

![](./Travel-Memory%20screenshot_images/image-022.png)

build

![](./Travel-Memory%20screenshot_images/image-023.png)

We can see the build fpolder

![](./Travel-Memory%20screenshot_images/image-024.png)

Copy build to ngix

![](./Travel-Memory%20screenshot_images/image-025.png)

Configure nginx

![](./Travel-Memory%20screenshot_images/image-026.png)

![](./Travel-Memory%20screenshot_images/image-027.png)

![](./Travel-Memory%20screenshot_images/image-028.png)

Create AMIs

![](./Travel-Memory%20screenshot_images/image-029.png)

![](./Travel-Memory%20screenshot_images/image-030.png)

Create Target Group

![](./Travel-Memory%20screenshot_images/image-031.png)

![](./Travel-Memory%20screenshot_images/image-032.png)

**PHASE 5 — CREATE LOAD BALANCERS - ALB (Application Load Balancer)**

![](./Travel-Memory%20screenshot_images/image-033.png)

![](./Travel-Memory%20screenshot_images/image-034.png)

![](./Travel-Memory%20screenshot_images/image-035.png)

![](./Travel-Memory%20screenshot_images/image-036.png)

![](./Travel-Memory%20screenshot_images/image-037.png)

LB for frontend created

![](./Travel-Memory%20screenshot_images/image-038.png)

Creating LB for Backend

![](./Travel-Memory%20screenshot_images/image-039.png)

![](./Travel-Memory%20screenshot_images/image-040.png)

![](./Travel-Memory%20screenshot_images/image-041.png)

LB for backend is created.

![](./Travel-Memory%20screenshot_images/image-042.png)

We can see two Load Balancers are now created.

![](./Travel-Memory%20screenshot_images/image-043.png)

Purchase domain from any domain provider.

Then add my recently purchased Domain Go: CLOUDFLARE.COM

Add your domain.

update nameservers

Add DNS Records

**Frontend domain**

Type: CNAME

Name: @

Value: FRONTEND-ALB-DNS

**Backend domain**

Type: CNAME

Name: api

Value: BACKEND-ALB-DNS

![](./Travel-Memory%20screenshot_images/image-044.png)

**IMPORTANT CHANGE**

Frontend should NOT call backend public IP anymore. Use cloudflare DNS record name containing backend load balance DNS.

**Update frontend .env file**

**![](./Travel-Memory%20screenshot_images/image-045.png)**

**Rebuild frontend**

npm run build

Copy again: sudo cp -r build/\* /usr/share/nginx/travelmemory/

Restart nginx: sudo systemctl restart nginx

![](./Travel-Memory%20screenshot_images/image-046.png)

![](./Travel-Memory%20screenshot_images/image-047.png)

![](./Travel-Memory%20screenshot_images/image-048.png)