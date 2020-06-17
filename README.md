
# Prerequisites for the Lab

- Internet Access
- PC with at least:
  - 4 Core CPU
  - 8GB of RAM / 16GB recommended (16GB needed for the Istio Lab)
  - 40GB of free Disk Space





### Getting set up

Before we dive into the Labs, you need to be able to run the provided Lab VM. It contains a Minikube cluster and all the configurations for the subsequent labs. 


<div style="page-break-after: always;"></div>

# Part 1 - Install Hypervisor

Before we dive into the Labs, you need to be able to run the provided Lab VM. It contains a Minikube cluster and all the configurations for the subsequent labs.

> VMWare is the preferred option as it handles nested virtualization that we need for this lab very well.
VirtualBox has this option in the latest releases but might prove unstable on certain PCs/Macs (especially the MacBook Pro 16' seems to run into problems).

## Option 1 - Installing VMWare (preferred)

If you do not already have VMWare installed, install a 60 days trial for your OS now:

* macOS	[VMWare](https://www.vmware.com/products/fusion/fusion-evaluation.html)
* Windows	[VMWare](https://www.vmware.com/products/workstation/workstation-evaluation.html)



## Option 2 - Installing VirtualBox


If you do not already have VirtualBox installed, install it for your OS now:

It is important that you use a version equal or newer than 6.1.6!

* macOS	[VirtualBox](https://www.virtualbox.org/wiki/Downloads), VMware Fusion, HyperKit
* Linux	[VirtualBox](https://www.virtualbox.org/wiki/Downloads), KVM
* Windows	[VirtualBox](https://www.virtualbox.org/wiki/Downloads), Hyper-V

    
<div style="page-break-after: always;"></div>

## Part 2 - Download the Lab VM on your PC

The VM is an 13GB zip file that has to be downloaded.



### Option 1: Download with Aspera (recommended)

The easiest way to download the file is with IBM Aspera high-speed transfer solution.

Download it here:


[Aspera VMWare](https://aspera.pub/zM7YiFk/k8s_training)


[Aspera VirtualBox](https://aspera.pub/zM7YiFk/k8s_training)


### Option 2: Download from Google Drive (not recommended)

You can also download it from Google Drive, which is **much** slower.

Download it here (VirtualBox only):

[Google Drive VirtualBox](https://drive.google.com/drive/folders/12YFacjjc92Ens-XEecqgmOG9d0YCz4IQ?usp=sharing)




<div style="page-break-after: always;"></div>

## Part 3 - Starting the VM


### VMWare 

1. Open the VM by double-clicking on the Training2020.vmx file.

2. Start the VM from the VmWare interface.


### VirtualBox 

**IMPORTANT**: There have been problems reported running VirtualBox and Docker Desktop on Mac at the same time.
If you have Docker Desktop running please shut it down first, we'll use Docker in the VM.

1. Open the VM by double-clicking on the Training2020.vbox file.

2. Start the VM from the VmWare interface.


<div style="page-break-after: always;"></div>

## Part 4 - Testing the VM

1. When the VM is up and running you can login with

   User: training

   Pwd: passw0rd

2. You can now open the Firefox browser in the VM and check that you can open a webpage (google.com for example)

3. Open a terminal window (in the dock)



4. Execute the following commands to initialize your Training Environment
   
	
	```bash
	./welcome.sh
	```
	
	This will
	* 	pull the latest example code from my GitHub repository
	* 	start minikube if not already running
	* 	installs the registry
	* 	installs the Network Plugin (Cilium)
	* 	starts the Personal Training Environment
	
	> During this you will have to provide a name (your name) that will be used to show your progress in the Instructor Dashboard in order to better assist you.
	
	

<div style="page-break-after: always;"></div>


## Part 5 - Troubleshooting

1. If the startup script doesn’t work you can run ./resetEnvironment.sh (this can take up to 30 minutes as it has to redownload all Docker images)

2. If you lose your PTE Webpage just run minikube service student-ui

3. Problems on Windows 10

	Can be fixed in most cases by turning off Hyper-V by running (as admin): 
	`bcdedit /set hypervisorlaunchtype off`and rebooting.

	This disables Hyper-V and allows Virtualbox to support nested virtualisation.
	
	You can turn it back on again with `bcdedit /set hypervisorlaunchtype auto`

