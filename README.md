CONTAINERIZATION AND CONTAINER ORCHESTRATION

## Project Scenario
In this project, I will be containerizing a simple static website (HTML & CSS) for a company's sign-up page. This application will be containerised using docker, deployed to kubernetes cluster and accessed using nginx.

## Project Objectives
1. Setup  dicrectory and create html & css files
2. Implement with git
3. Dockerize the application
4. Push to Docker hub
5. Setting up and using Kubernetes Cluster
6. Accessing Deployed Application

## Step 1: Setup and Git Initialization
## Tasks:
1. Create a new project directory.
```bash
mkdir 06.Containerization-and-Container-Orchestration-using-Docker-Kubernetes
```
2. Create a new `index.html` file and use text editor vim to add the code to the file.
```bash
touch index.html
vim index.html 
```

Paste the code below
```bash
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<!-- displays site properly based on user's device -->

		<link
			rel="icon"
			type="image/png"
			sizes="32x32"
			href="./img/favicon-32x32.png"
		/>

		<title>Responsiveness and Media Queries</title>

		<link rel="stylesheet" href="style.css" />
	</head>
	<body>
		<div class="container">
			<div>
				<h1>
					Learn to code by
					<br />
					watching others
				</h1>
				<p>
					See how experienced developers solve problems in real-time. Watching
					scripted tutorials is great, but understanding how developers think is
					invaluable.
				</p>
			</div>
			<div>
				<div class="box box-blue">
					<p>
						<strong>Try it free 7 days</strong>
						then $20/mo. thereafter
					</p>
				</div>

				<form class="box" id="form">
					<div class="form-control">
						<input type="text" id="firstname" placeholder="First Name" />
						<img src="./img/icon-error.svg" alt="error-icon" />
						<small></small>
					</div>
					<div class="form-control">
						<input type="text" id="lastname" placeholder="Last Name" />
						<img src="./img/icon-error.svg" alt="error-icon" />
						<small></small>
					</div>
					<div class="form-control">
						<input type="email" id="email" placeholder="Email Address" />
						<img src="./img/icon-error.svg" alt="error-icon" />
						<small></small>
					</div>
					<div class="form-control">
						<input type="password" id="password" placeholder="Password" />
						<img src="./img/icon-error.svg" alt="error-icon" />
						<small></small>
					</div>

					<button>Claim your free trial</button>
					<small>
						By clicking the button, you are agreeing to our
						<a href="#">Terms and Services</a>
					</small>
				</form>
			</div>
		</div>

	</body>
</html>
```

3. Create a new `style.css` file and use text editor vim to add the code to the file.

```bash
touch style.css
vim style.css 
```
Paste the code
```bash
@import url('https://fonts.googleapis.com/css?family=Poppins:400,500,600,700&display=swap');

* {
	box-sizing: border-box;
}

body {
	background-color: hsl(0, 100%, 74%);
	background-image: url('./images/bg-intro-desktop.png');
	color: #fff;
	font-family: 'Poppins', sans-serif;
}

.container {
	display: flex;
	align-items: center;
	justify-content: center;
	flex-wrap: wrap;
	max-width: 1200px;
	margin: 0 auto;
	min-height: 100vh;
}

.container > div {
	flex: 1;
	padding: 0 20px;
}

h1 {
	font-size: 40px;
	line-height: 50px;
}

p {
	font-size: 15px;
	opacity: 0.8;
}

.box {
	background-color: #fff;
	border-radius: 5px;
	box-shadow: 0 6px rgba(0, 0, 0, 0.2);
	padding: 30px;
	margin-bottom: 20px;
	text-align: center;
}

.box p {
	margin: 0;
}

.box-blue {
	background-color: hsl(248, 32%, 49%);
	padding: 20px;
}

.form-control {
	position: relative;
	margin-bottom: 30px;
}

.form-control small {
	color: hsl(0, 100%, 74%);
	font-weight: 600;
	position: absolute;
	bottom: -24px;
	right: 0;
	opacity: 0;
	text-align: right;
}

input {
	border-radius: 5px;
	border: 1.3px solid hsl(246, 25%, 77%);
	font-family: 'Poppins', sans-serif;
	font-size: 14px;
	font-weight: 500;
	padding: 15px 25px;
	display: block;
	width: 100%;
}

.form-control.error input {
	border-color: hsl(0, 100%, 74%);
	color: hsl(0, 100%, 74%);
}

.form-control.error input::placeholder {
	color: hsl(0, 100%, 74%);
}

input:focus {
	border: 1.3px solid hsl(248, 32%, 49%);
	outline: none;
}

.form-control img {
	opacity: 0;
	position: absolute;
	top: 50%;
	right: 15px;
	transform: translateY(-50%);
	height: 20px;
}

.form-control.error img {
	opacity: 1;
}

button {
	background-color: hsl(154, 59%, 51%);
	border-radius: 5px;
	border: 1px solid hsl(154, 59%, 45%);
	box-shadow: 0 2px hsl(154, 59%, 45%);
	color: #fff;
	cursor: pointer;
	display: block;
	font-family: 'Poppins', sans-serif;
	font-size: 14px;
	font-weight: 500;
	padding: 15px 25px;
	letter-spacing: 1px;
	text-transform: uppercase;
	width: 100%;
}

button:focus {
	outline: none;
}

button:active {
	box-shadow: 0 0 hsl(154, 59%, 45%);
	transform: translateY(2px);
}

.form-control small {
	opacity: 0;
}

.form-control.error small {
	opacity: 1;
}

small {
	display: block;
	color: #bbb;
	font-size: 11px;
	font-weight: 500;
	margin-top: 15px;
}

small a {
	color: hsl(0, 100%, 74%);
	font-weight: 600;
	text-decoration: none;
}

@media screen and (max-width: 768px) {
	h1 {
		text-align: center;
	}

	p {
		text-align: center;
	}

	.container {
		flex-direction: column;
	}
}
```

4. Git add, commit & push the files created to github.
```bash
git add .
git commit -m "Added files"
git push
```


## Step 2: Dockerize the Application
I decided to containerize and orchestrate the application on an EC2 instance. I creeated an instance, started it and connected to it.

SSH into Ec2 instance.


## Tasks:
1. Creating dockerfile.
- I created a directory named `capstone` (directory for index.html file & dockerfile).
- In the capstone directory created, I created another directory called Signup_page where the index.html & style.css files were stored.
- Create a dockerfile in the capstone directory.

```bash
touch dockerfile
vim dockerfile
```


In the dockerfile specify nginx as the base image & copy index.html and the styles.css into the Nginx HTML directory.
![](./images/04.vi%20dockerfile.png)

### Breakdown of the Dockerfile above

This Dockerfile sets up a Docker image based on NGINX, a popular web server.

-  `FROM nginx`: This line specifies that we are using the official NGINX Docker image as the base image for our container. This means that our container will include all the necessary files and configurations to run NGINX.

-  `WORKDIR /usr/share/nginx/html`: This command sets the working directory within the NGINX container to /usr/share/nginx/html. This directory is typically where NGINX serves static HTML files from.

-  `COPY webapp`: This line copies the contents in that folder which is the index.html file & style.css file in the Signup_page directory from the build context (the directory where the Dockerfile is located) into the /usr/share/nginx/html directory within the container. 

- `EXPOSE 80`: This command exposes port 80 on the container. Port 80 is the default port for HTTP traffic, so by exposing it, we allow external clients to access our NGINX server running inside the container.

Overall, this Dockerfile is setting up a basic NGINX server with custom HTML (index.html) and CSS (styles.css) files served from the /usr/share/nginx/html directory, and it exposes port 80 to allow external access to the NGINX server.

2. Create/Build an image- ensuring you have Docker Desktop installed. If you are working on an EC2 instance, ensure Docker is installed on it. In my scenario, I am using my EC2 instance so i installed it in my instance.

Build an image using the dockerfile just created.
```bash
docker build -t dockerfile .
```


3. Check the images list to verify the dockerfile image is already created
```bash
docker images 
```


4. Run a container based on the image created and map it to a listening port
```bash
docker run -p 8080:80 dockerfile
```


5. Check the list of available containers. Start a container and confirm it's running.
```bash
docker ps -a
docker start 
docket ps
```


6. Copy and paste the EC2 instance public IP Address including the port to view the webpage.

![
![](./images/11.using%20ip-address%20and%20port%2080.png)

## Step 3: Push to Dockerhub
## Tasks:

1. Tag image! I already have a dockerhub account, I'll tag my image using my username and repository name then push.
```bash 
docker tag dockerfile webapp
```


2. Login to docker hub
```bash
docker login -u username
```


3. Push the image to docker hub
``` bash
docker push webapp


## Step 4: Set up a Kind Kubernetes Cluster

This setup is to DEPLOY IMAGE TO KUBERNETES CLUSTER.

Kind runs Kubernetes clusters in Docker containers, so you will need Docker installed. I already have docker installed in my EC2 instance. 


## Tasks:
1. Install Kind (Kubernetes in Docker) & verify kind version
```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```
```bash
kind version
```


2. Create a Kind Cluster
- Create a directory capstone-kind

cd into the directory

Run the command to create a Kind cluster:
```bash
 kind create cluster
```

This command will create a single-node Kubernetes cluster using Kind.

After creating cluster, you can verify that the cluster is running by executing:
```bash
kubectl cluster-info
```




3. Install kubectl
```bash
sudo snap install kubectl --classic
```


4. Configure kubectl to point to the kind cluster

```bash
kubectl cluster-info --context kind-kind
```



5. Get cluster nodes
```bash
kubectl get nodes
```


## Step 5: Deploy to Kubernetes
## Tasks:
1. Create a Kubernetes YAML file. 

Write a Kubernetes Deployment configuration in a YAML file. This file describes the desired state for your application pods.
```bash
touch kub-deployment.yaml
vim kub-deployment.yaml
```


This YAML configuration defines a Kubernetes Deployment named `webapp` that manages a single replica of a containerized application. Let's break it down:

`apiVersion`: apps/v1: This specifies the API version being used. In this case, it's apps/v1, which is commonly used for managing higher-level abstractions like Deployments, StatefulSets, and DaemonSets.

`kind`: Deployment: Defines the type of Kubernetes resource being created, which is a Deployment. A Deployment manages a set of identical pods, ensuring that a specified number of them are running at any given time.

`metadata`: Contains metadata about the Deployment, such as its name.

`name`: webapp: The name of the Deployment.
`spec`: Describes the desired state of the Deployment, including how many replicas of the application should be running and how to define the pods.

`replicas:` 1: Specifies that there should be one replica of the application running. Kubernetes will ensure that this many instances of the application are running at all times.

`selector`: Defines how the Deployment selects which pods to manage.

`matchLabels:` Specifies that the Deployment should manage pods with the label app: signup-page
template: Specifies the pod template that Kubernetes will use to create new pods.

`metadata`: Contains metadata for the pods created from this template.

`labels`: Specifies the labels to be applied to the pods. In this case, the label app: `signup-page` is applied.
`spec`: Specifies the specification for the containers within the pod.

`containers`: Describes the containers that should be run in the pod.

`name`: `webapp-container`: The name of the container.

`image`: slarry07/webapp:lastest Specifies the Docker image to use for the container. The image devoyinda/capstone_proj_6_doc_and_kub is being used with the 1.0 tag, indicating the version of the image - This is the image we pushed to the dockerhub.

`ports`: Specifies the ports to expose on the container.

`containerPort`: 80: Specifies that port 80 within the container should be exposed. This allows traffic to reach the application running inside the container.


2. Create Service YAML File - Write your Kubernetes Service configuration in a YAML file. This file exposes your application to network traffic.

```bash
touch kub-service.yaml
vim kub-service.yaml
```


3. Apply the deployment and service to the cluster
```bash
kubectl apply -f kub-deployment.yaml
kubectl apply -f service.yaml
```



4. Verify Deployment and Service - After applying the YAML files, you can verify that the resources have been created successfully by running:
```bash
kubectl get deployments
kubectl get service
```

![](./images/25.%20verify%20deployment%20&%20services%20running.png)


## Step 7: Access the Application
## Task
1. Port forward the service to access the application locally.

Once you have identified the pod, you can use the kubectl port-forward command to forward a local port to a port on the pod.

`kubectl port-forward <pod-name> <local-port>:<pod-port>`

Replace `<pod-name>` with the name of your pod, `<local-port>` with the port on your local machine you want to use to access the application, and `<pod-port>` with the port your application is listening on within the pod.

```bash
 kubectl port-forward --address 0.0.0.0 service/myweb-service 8081:80
```
<img width="894" height="215" alt="image" src="https://github.com/user-attachments/assets/c608eaaf-85d0-40da-914f-f13475c5ec9e" />


2. Access the website through your browser on port 8080

In your browser, visit http://localhost:8080 to view your static website.




![](./images/29.%20check%20port%2080.png)
