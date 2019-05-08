# IBM Kubernetes Training

Before attending the workshop, you need to complete the following 4 steps. 


---
---

# Part 1 - Setting up Minikube

### Getting set up


----

## Install a Hypervisor

If you do not already have a hypervisor installed, install one for your OS now:

Operating system	Supported hypervisors:

* macOS	[VirtualBox](https://www.virtualbox.org/wiki/Downloads), VMware Fusion, HyperKit
* Linux	[VirtualBox](https://www.virtualbox.org/wiki/Downloads), KVM
* Windows	[VirtualBox](https://www.virtualbox.org/wiki/Downloads), Hyper-V

    Note: Minikube also supports a --vm-driver=none option that runs the Kubernetes components on the host and not in a VM. Using this driver requires Docker and a Linux environment but not a hypervisor.
    
---

## Install Minikube on your OS


### macOS

Requires installing a hypervisor, such as [hyperkit](https://github.com/kubernetes/minikube/blob/master/docs/drivers.md#hyperkit-driver) (recommended) or VirtualBox.

The easiest way to install Minikube on macOS is using Homebrew:

```
# Install brew
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

#Install minikube
$ brew cask install minikube

```


Or if you don't want to use **brew**

```
$ curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64 \
  && chmod +x minikube

$ sudo mv minikube /usr/local/bin
```


---

### Linux
  * Requires either the [kvm2 driver](https://github.com/kubernetes/minikube/blob/master/docs/drivers.md#kvm2-driver) (recommended), or VirtualBox
  * VT-x/AMD-v virtualization must be enabled in BIOS
  * manually:  `curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && sudo install minikube-linux-amd64 /usr/local/bin/minikube`

---

### Windows 10
  * Requires a hypervisor, such as VirtualBox (recommended) or HyperV
  * VT-x/AMD-v virtualization must be enabled in BIOS
  * using [chocolatey](https://chocolatey.org/) `choco install minikube`
  * manually: Download and run the [installer](https://storage.googleapis.com/minikube/releases/latest/minikube-installer.exe)

---


# Starting minikube (all macOS, Windows and Linux)

Then we start minikube (parameters are important for the Istio Lab):

```
$ minikube start --vm-driver virtualbox --memory=8192 --cpus=4                                                                                                                                              

😄  minikube v1.0.1 on darwin (amd64)
💿  Downloading Minikube ISO ...
 113.03 MB / 142.88 MB [=================================>--------]  79.11% 1m6s
 
 ...
 
😄  minikube v1.0.1 on darwin (amd64)
🤹  Downloading Kubernetes v1.14.1 images in the background ...
💡  Tip: Use 'minikube start -p <name>' to create a new cluster, or 'minikube delete' to delete this one.
🔄  Restarting existing virtualbox VM for "minikube" ...
⌛  Waiting for SSH access ...
📶  "minikube" IP address is 192.168.99.100
🐳  Configuring Docker as the container runtime ...
🐳  Version of container runtime is 18.06.3-ce
⌛  Waiting for image downloads to complete ...
✨  Preparing Kubernetes environment ...
🚜  Pulling images required by Kubernetes v1.14.1 ...
🔄  Relaunching Kubernetes v1.14.1 using kubeadm ...
⌛  Waiting for pods: apiserver proxy etcd scheduler controller dns
📯  Updating kube-proxy configuration ...
🤔  Verifying component health .....
💗  kubectl is now configured to use "minikube"
🏄  Done! Thank you for using minikube!

```

Wait for minikube to start this may take some time to download and start the cluster.



If you need some more details: [Install MiniKube](https://kubernetes.io/docs/tasks/tools/install-minikube/)


---
---
---

# Tips and Tricks for 

**Hint**

Ir you want to use hyperkit you have to install it with

```
$ brew install hyperkit
$ brew install docker-machine-driver-hyperkit
$ sudo chown root:wheel /usr/local/bin/docker-machine-driver-hyperkit && sudo chmod u+s /usr/local/bin/docker-machine-driver-hyperkit
```

And start minikube with

```
$ minikube start --vm-driver hyperkit --memory=8192 --cpus=4                                                                                                                                              
```





**Hint:**

IF you get the following error:
💣 Error starting cluster: wait: waiting for component=kube-apiserver: timed out waiting for the condition

Try deactivating your VPN (Cisco AnyConnect, ...) and/or reboot.

---

**Hint:**

If needed you can specify the VM provider:

`minikube start --memory=8192 --cpus=4 --vm-driver=virtualbox`


`minikube start --memory=8192 --cpus=4 --vm-driver=vmwarefusion`

---

**Hint:**

If you have previously installed minikube, and run:

`minikube start`

And the command returns an error:

`machine does not exist`

You need to wipe the configuration files:

`rm -rf ~/.minikube`



# Part 2 - Download the Kubernetes CLI

To interact with your cluster, you will need to install the Kubernetes CLI that corresponds to your operating system and minikube version:



**For Windows users:** 

Manual install 

* [Download for Windows](https://storage.googleapis.com/kubernetes-release/release/v1.14.0/bin/windows/amd64/kubectl.exe)
* And add the binary in to your PATH.

or using [chocolatey](https://chocolatey.org/) 
```
choco install kubernetes-cli
```

---

**For OS X and Linux users:**

#### Install via command line (preferred)

```
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.14.0/bin/darwin/amd64/kubectl

$ mv ./kubectl /usr/local/bin/kubectl

$ chmod +x /usr/local/bin/kubectl


```



#### Direct download

Download from:

* [OS X](https://storage.googleapis.com/kubernetes-release/release/v1.10.8/bin/darwin/amd64/kubectl)
* [Linux](https://storage.googleapis.com/kubernetes-release/release/v1.10.8/bin/linux/amd64/kubectl)

1. Move the executable file to the `/usr/local/bin` directory using the command `mv /<path_to_file>/kubectl /usr/local/bin/kubectl` .

2. Make sure that `/usr/local/bin` is listed in your PATH system variable.

	```
	$ echo $PATH
	/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
	```

3. Convert the binary file to an executable: `chmod +x /usr/local/bin/kubectl`






# Part 3 - Install Git on your laptop

To do so : 

For MacOS :
http://mac.github.com

For Windows: 
http://git-scm.com/download/win

At some point during the installation, change to the **"Use Windows default console"** and continue the installation.
![Git for Windows](./images/git2.png)



# Part 4 - Check if everything works as expected


## 1. Check kubectl 

	type the following command :
	
	`kubectl version --short`
	
And you should check that you are using the same version as the kubernetes verson running in minikube. 

The `client verson` should match the `server version`:


	```
	$ kubectl version                                                                                          
	
	Client Version: version.Info{Major:"1", Minor:"14", GitVersion:"v1.14.0", GitCommit:"641856db18352033a0d96dbc99153fa3b27298e5", GitTreeState:"clean", BuildDate:"2019-03-25T15:53:57Z", GoVersion:"go1.12.1", Compiler:"gc", Platform:"darwin/amd64"}
	Server Version: version.Info{Major:"1", Minor:"14", GitVersion:"v1.14.1", GitCommit:"b7394102d6ef778017f2ca4046abbaa23b88c290", GitTreeState:"clean", BuildDate:"2019-04-08T17:02:58Z", GoVersion:"go1.12.1", Compiler:"gc", Platform:"linux/amd64"}
	 ```
		
	

## 1. Check git 

	type the following command :
	
	`git version `
	
	And you should get something similar :
	
	```
	$ git version                                                                                                                         
	git version 2.18.0
	```



