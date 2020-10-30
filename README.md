### Simple project for Codemi with Node.js App

### Overview of the App :

- App build with Node.js
- How to test app :

  ```$ curl http://(IP-Address:30001/)``` 

  >>> result : Hello Codemi !!!

- app source :
  /nodejs-web/app.js

### 1. Dockerize nodejs-web
 
  ``` $ docker build -t dionmadyasta/nodejs-web:1 .```

### 2. Kubernetes Manifest for Deployment

  deployment.yaml
 
 -  ```$ kubectl apply -f deployment.yaml ```
 -  ```$ kubectl get all ```
 -  ```$ minikube service nodejs-web-service ``` 
  
### 3. Summary

####    a.  Deployment

- I've used ```dionmadyasta/nodejs-web:1``` for the docker image that will be run in deployment
- and ```dionmadyasta/nodejs-web:1``` has been pushed on the docker-hub

####    b.  Service

- Set target port to 3000 and node port to 30001
- So we can expose the application using port 30001

####  c.  HPA (HorizontalPodAutoscaler)

- When the application is deployed, it will create a minimum of 2 nodes and maximum of 5 nodes
- We use the ```Utilization``` scenario type for CPU and Memory trigger

      CPU : 
      - If the CPU utilization reaches an average of 70%, the HPA will automatically scale up the node
      - If the CPU utilization at the next node still reaches 70%, it will scale up continuously until it reaches a maximum total of maxReplicas: 5
      - And will scale down if the CPU utilization is less than 70%, to at least 2 nodes

      Memory :
      - If the Memory utilization reaches an average of 70%, the HPA will automatically scale up the node
      - If the Memory utilization at the next node still reaches 70%, it will scale up continuously until it reaches a maximum total of maxReplicas: 5
      - And will scale down if the Memory utilization is less than 70%, to at least 2 nodes



### 4. Thanks !!!