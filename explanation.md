## Deploy react WebApp (Yolo) to Kubernates

## Implementation plan

 ## prerequisites 
  1. Docker Desktop installation is completed.
  2. Minikube is installed and running within Docker Desktop.

## Step 1
 Build two images: one for the backend and another for the client, then push them to Docker Hub.

## Step 2 
 Develop deployment files for both the backend and client components.

## Step 3
Generate two services, corresponding to the backend and client services.

## Step 4
For securely managing your MongoDB URL, create a secret file. If you're using a remote connection, this step might not be necessary. In the case of a deployed MongoDB within Kubernetes (as in my scenario), create deployment and service files, and include secrets for your MongoDB username and password.

## Step 5
 Execute the deployment with the following command:

`
kubectl apply -f <filename>
`

Apply the files in the following sequence:

1. secrets file
2. Deployment files
3. Service files

## Step 6
Accessing backend and the client

I've successfully created two services, namely `ipweek2-client-service` and `ipweek2-backend-service`, which play a vital role in enabling external access to both my client and backend applications. By specifying selectors, I've precisely targeted Pods labeled as `app: ipweek2-client` and `app: ipweek2-backend`. The type of service I've chosen is `LoadBalancer`, letting the cloud provider manage the intricacies of load balancers. These load balancers efficiently handle incoming external traffic and expertly direct it to the specific Pods selected earlier. I've configured the services to seamlessly guide incoming traffic on ports 3000 and 5000 to the corresponding ports on the Pods. This thoughtful setup guarantees that external users can conveniently engage with both my client and backend applications via the externally assigned IP address or hostname. Furthermore, I've established an intriguing connection between my client and backend applications. By leveraging the Pod IPs from the backend, I've empowered the client to effectively communicate with the backend using these exposed IP addresses. This strategic arrangement not only enables external users to interact seamlessly with both applications but also fosters a smooth and collaborative interaction between my client and backend, thanks to the exposed IPs.

For backend use below command

`
kubectl apply -f ipweek2-backend-service.yaml
`

For client to be able to access the client service in your browser

`
kubectl apply -f ipweek2-client-service.yaml
`

## Step 7

Access the client app using this [url](http://localhost:3000) and you can add, edit, delete and view the products.

minikube service ipweek2-client-service 

minikube service ipweek2-backend-service 


## Choice of kubernetes Objects

I've made strategic decisions by employing Deployments to manage my backend and client applications. This choice is grounded in the fact that Deployments excel in handling stateless applications, like my backend and client apps. They simplify the scaling process and updates, making horizontal scaling easy while abstracting away complexities.

 I've utilized a StatefulSet configuration for my MongoDB service, a choice backed by its stateful nature. The stable network identities and consistent storage provided by StatefulSets align perfectly with MongoDB's requirements. Maintaining these aspects is pivotal for preserving data consistency and accessibility.


