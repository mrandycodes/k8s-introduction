# k8s-introduction

## Installing Minikube

The Minikube tool source code with all the documentation is available at GitHub at (https://github.com/kubernetes/minikube)[https://github.com/kubernetes/minikube]

### Installing on Mac

The following sequences of commands will download the minikube binary, set the executable flag and copy it to the `/usr/local/bin` folder, which will make it available in the macOS shell:

````
$ curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.12.2/minikube-darwin-amd64
$ chmod +x minikube
$ sudo mv minikube /usr/local/bin/  
````

Alternatively, if you use Homebrew package manager (available freely at (https://brew.sh)[https://brew.sh]), which is, by the way, very handy and recommended, you can just install minikube by typing:

````
$ brew cask install minikube
````

### Installing on Windows

Minikube for Windows is also simply a single executable file. You can always find the newest version on the Minikube's site, at (https://github.com/kubernetes/minikube)[https://github.com/kubernetes/minikube]. You just need to download the latest executable, rename it minikube.exe, and place it in your system path to have it available from the command line.