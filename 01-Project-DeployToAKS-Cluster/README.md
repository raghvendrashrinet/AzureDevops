### Related  Github Action Project 

- [raghvendrashrinet helsinki-cloud-native](https://github.com/raghvendrashrinet/helsinki-cloud-native/tree/main/Kubernetes/Chapter-4%20Cloud/GitHub%20Actions-Pipeline)

### Azure Devops Portal Link 

- https://dev.azure.com/raghvendrashrinate


---

### Setup local agent (runner)
Org-> Seting -> agents -> new agent -- will prompt to setupagent as below 
Configure your account by following the steps outlined here.
- Download the agent
- Create the agent
```
PS C:\> mkdir agent ; cd agent
PS C:\agent> Add-Type -AssemblyName System.IO.Compression.FileSystem ; [System.IO.Compression.ZipFile]::ExtractToDirectory("$HOME\Downloads\vsts-agent-win-x64-5.277.0.zip", "$PWD")
```
- Configure the agent

```
PS C:\agent> .\config.cmd
```
Optionally run the agent interactively
If you didn't run as a service above:
```
PS C:\agent> .\run.cmd
```

