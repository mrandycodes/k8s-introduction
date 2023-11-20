# k8s-introduction

## Installing Minikube

The Minikube tool source code with all the documentation is available at GitHub at <https://github.com/kubernetes/minikube>

### Installing on Mac

The following sequences of commands will download the minikube binary, set the executable flag and copy it to the `/usr/local/bin` folder, which will make it available in the macOS shell:

``````
$ curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.12.2/minikube-darwin-amd64
$ chmod +x minikube
$ sudo mv minikube /usr/local/bin/  
``````

Alternatively, if you use Homebrew package manager (available freely at <https://brew.sh>), you can just install minikube by typing:

``````
$ brew cask install minikube
``````

### Installing on Windows

Minikube for Windows is also simply a single executable file. You can always find the newest version on the Minikube's site, at <https://github.com/kubernetes/minikube>. You just need to download the latest executable, rename it minikube.exe, and place it in your system path to have it available from the command line.

### Starting up the local Kubernetes cluster

We're using the local Kubernetes cluster provided by minikube. Start your cluster with:

``````
$ minikube start 
``````

As the cluster is running now and we have the dashboard addon enabled by default, you can take a look at the (still empty) Kubernetes dashboard with the following command:

``````
$ minikube dashboard
``````

It will open your default browser with the URL of the cluster's dashboard

## Installing kubectl

### Installing on Mac

The following sequences of command will download the kubectl binary, set the executable flag and copy it to `/usr/local/bin` folder which will make it available in the macOS shell:

``````
$ curl -O https://storage.googleapis.com/kubernetes-release/release/v1.5.2
/bin/darwin/amd64/kubectl
$ chmod +x kubectl
$ sudo cp kubectl /usr/local/bin  
``````

Homebrew provides the most convenient way to install kubectl and keep it up to date. To install, use this command:

``````
$ brew install kubectl
``````

To update, use the following command:

``````
$ brew upgrade kubectl
``````

### Installing on Windows

You can find the list of Windows kubectl releases on GitHub at <https://github.com/eirslett/kubectl-windows/releases>. Similar to Minikube, kubectl is just a single .exe file. At the time of writing this book it's <https://github.com/eirslett/kubectl-windows/releases/download/v1.6.3/kubectl.exe>. You will need to download the exe file and place in on your system path, to have it available in the command line.

## Our first deployment

Take a look over the demo spring boot application that we have prepared for you, you'll find inside a `Dockerfile`, a `deployment.yml` and a `service.yml`; Let's review them for a moment.

Now to perform our first k8s deployment we need to package our app fist. To package, use the following command:

``````
$ mvn package
``````

Then build a docker image of our application, use the following command:

``````
$ docker build -t demo:latest .
``````

In order to use your docker image, you will need to push this image into your personal docker hub repository. To do that you will need to login into <https://hub.docker.com/> inside of your local docker application.
Then you'll be able to run the following commands:

``````
$ docker login -u "myusername" -p "mypassword" docker.io
$ docker tag demo myusername/demo
$ docker push myusername/demo
``````

Finally, use the following command to do your first k8s deployment:

``````
$ kubectl apply -f deployment.yml
$ kubectl apply -f service.yml
``````

Test your service with curl or postman but first expose a port in your local machine:

``````
$ kubectl port-forward service/demo 7080:80
``````