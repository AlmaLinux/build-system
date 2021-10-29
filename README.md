# About AlmaLinux Build System

What is AlmaLinux Build System? AlmaLinux Build System is a project designed to automate processes of building distribution and packages, testing packages, signing packages, and releasing them to public repositories.
The general purpose of the AlmaLinux Build System is to minimize manual work in order to reduce the amount of human-caused mistakes.
We started to develop our product in 2012 for CloudLinux OS building and automatization. Specifically for AlmaLinux's other projects KernelCare and Imunify360 support, we launched the ability to build and test deb packages type.
Besides being used for typical testing scenarios, AlmaLinux Build System is integrated with Jenkins for complicated scenarios. 

# Why we did our own?

The main reason is to help our quickly-growing team and new-coming employees to learn how to build and test rpm packages faster and easier. 
As well, the support of deb packaged was required. So AlmaLinux needed an integrated pipeline for all the distribution maintenance processes: building, testing, signing and releasing packages. To manage all these phases together, not separately, successfully and effectively we created AlmaLinux Build System.

# Development 

![image](images/Build-System-Diagram.jpg)

* [**Build System's Master Service**](https://github.com/AlmaLinux/build-system) interacts via [API](https://github.com/AlmaLinux/albs-web-server) interface with UI and CLI tools. 
* [**Build Node**](https://github.com/AlmaLinux/albs-node) sends requests to the Master Service and receives Build Tasks to build packages. After being built these packages are kept as artifacts at the [**Artifact Storage**]((https://build.almalinux.org/pulp/content/builds/AlmaLinux-8-x86_64-22-br/)). 
* [**Test System**](https://github.com/AlmaLinux/alts) sends a request and receives Test Tasks (builds) to test built packages from Artefact Storage. Test System test packages via Test Nodes (eg. Docker or OpenNebula with different architectures) and send test artifacts or test logs and reports back to Artifact Storage.
* [**Sign Server**](https://github.com/AlmaLinux/albs-sign-node) sends a request and receives sign tasks to sign packages with our PGP key. It takes unsigned packages from Artifact Storage and puts them back signed.
* **Release System** sends a request and receives release tasks to upload signed packages to public repositories.
* [**Git Server**](git.almalinux.org) sends updates via API to Master Service. It does it with the help of two services: [gitea-listener](https://github.com/AlmaLinux/gitea-listener) and git-cacher

AlmaLinux Build System supports different architectures such as x86_64, aarch64 and ppc64le. 
Build system and test system are scalable. Also, their benefits are auto modification and debranding. 
We support several types of packages (also for Ubuntu and Debian).

# Reporting issues and track the progress

All issues should be reported to this project. A GitHub's [kanban board](https://github.com/orgs/AlmaLinux/projects/1) is used for the Build System project to track the progress.