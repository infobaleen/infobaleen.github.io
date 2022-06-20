# Table of Contents
1. [Creating new platform](#creating-new-platform)
1. [To access ib-kube:](#to-access-ib-kube)
[](#table-of-contents)

[*Back to top*](#table-of-contents)

# Creating new platform
- [ ] Open ib-kube repo
- [ ] Check customer’s domain name, match platform name with theirs
- [ ] Create new file in pkg/settings/k8s with name platformname.go
- [ ] Paste content from another platform with recent build
- [ ] Redefine:  
  - [ ] Var name to platform name  
  - [ ] Name:
  - [ ] Subdomain:
  - [ ] Check available ingress (max 15)
  - [ ] Ingress: to available ingress

- [ ] Follow ingress definition (Ctrl click Ingress variable)
- [ ] Copy ingress IP (used for dns record) (skicka IP till christian)
- [ ] Add/remove Args for centra or other integrations
- [ ] Verify tag (commit version)
- [ ] Adjust cpu limit and memory parameters if needed
- [ ] Save File

- [ ] Open pkg/setting/k8s/k8s.go
- [ ] Add variable for platform data to Platforms variable by appending to list
- [ ] Save File

- [ ] Open terminal  in VS code and run git pull
- [ ] Then run make yaml (ignore errors)

- [ ] Go to Source Control
- [ ] Commit your changes with message (e.g. “created platform _NAME_ on _COMMIT VERSION_”
- [ ] Push to repo

- [ ] [Request someone to] run “make k8s” 
- [ ] [Request someone to] add the DNS registry
- [ ] [Request someone to] add to k8s ml registry

[*Back to top*](#table-of-contents)

# To access ib-kube:
  * Install WSL 2  
    * https://pureinfotech.com/install-windows-subsystem-linux-2-windows-10/  
    * https://code.visualstudio.com/blogs/2019/09/03/wsl2  
  * Boot Ubuntu  
  * Install VS Code  
  * Git clone ib-kube  
  * Cd ib-kube  
  * Run command ``code .``  
  * Done  

[*Back to top*](#table-of-contents)
