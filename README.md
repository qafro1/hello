# app
Objective:

This approach to create a Python application within a Docker container and then load balance the application within Kubernetes (minikube).

Prerequisites

1. Docker machine
2. Docker Hub account for docker repo
3. Minikube for Kubernetes
4. kubectl

Documentation for the above are provided below:
<br> Docker: https://docs.docker.com/</br>
<br>Dockerhub: https://hub.docker.com/</br>
<br>minikube: https://kubernetes.io/docs/tasks/tools/install-minikube/</br>
<br>kubectl: https://kubernetes.io/docs/tasks/tools/install-kubectl/</br>

<br>Implementation</br>
Kubernetes coordinates a highly available cluster of computers that are connected to work as a single unit.
A Service in Kubernetes is an abstraction which defines a logical set of Pods and a policy by which to access them.
LoadBalancer - This provides an externally-accessible IP address that sends traffic to the correct port on your cluster nodes.

Diagram:

                                Kubernetes cluster 
<!-- Internet Traffic  ---------->| Loadbalancer|--------->| Services ------------>Pod1 & pod2                                                                                                                       


<br>Installing</br>
As discussed in the prerequisites the following needs to be checked or installed from the documentations provided.
However - This project is using a sample DockerHub account for repo to get started and recommends to create your own account then follow procedures for future useage.

<br>Configuration</br>
Check if docker is installed: docker --version,if not install docker: https://docs.docker.com/

Dockerhub: Docker Hub can automatically build images from source code in an external repository and automatically push the built image to your Docker repositories.
This project has been configured and setup it will be using docker image: qafro/<-docker image->

When you push code to a source code branch in GitHub for one of those listed image tags, the push uses a webhook to trigger a new build, which produces a Docker image. The built image is then pushed to the Docker Hub registry.
Documentation to Set up automated builds for docker: https://docs.docker.com/docker-hub/builds

<br>Create docker image from cli:</br>
1. docker login
2. docker images
3. docker tag local-image:tagname new-repo:tagname
4. docker push new-repo:tagname


Minikube & kubectl should be configured according to the Documentations.

<br>Testing</br>
In the dev environment - steps to run test locally.
1. Check if docker is installed: docker --version.
2. Run a clone of the project: git clone https://github.com/qafro1/hello.git or get source locally then change into that directory.
3. Build the app which build the image of app with tag python-hello: docker build -t python-hello .
4. Run the app locally: docker run --name python-hello -p 5000:5000 python-hello
5. Test the app if it's running successfully with port 5000: curl http://localhost:5000
6. Result display: Hello World...*


<br>Running</br>
This project will deploy python-hello python app to kubernetes cluster using minikube.
This section will get Minikube up running and deploy the kubernetes manifest files.
Assumming the Minikube & kubectl are configured.
Also the docker image used as stated: qafro/python-hello

To deploy it using minikube, we are using deploy.yaml and service.yaml configuration file, which will tell the Kubernetes cluster the configuration.
1. minikube server needs to run: minikube start
2. check the Minikube nodes to show minikube   Ready    master: kubectl get node
3. Create a deployment: kubectl apply -f deploy.yaml
4. Create a create a service: kubectl apply -f service.yaml
5. Check both kubernates deployment & service are running: kubectl get deploy,svc
6. To display the result in a browser: minikube service python-hello
7. Result display : Hello World...*



<br>Troubleshooting.</br>
<br>Debugging Pods</br>
Check the current state of the Pod and recent events with the following command: kubectl describe pods ${POD_NAME}
<br>View the state of the containers in the pod.</br>

<br>Pod is crashing or otherwise unhealthy</br>
Take a look at the logs of the current container: kubectl logs ${POD_NAME} ${CONTAINER_NAME}

