### Step 2: Create Required Service Connections
Your pipeline relies on two service connections defined in variables: azureServiceConnection (my-azure-connection) and dockerRegistryServiceConnection (my-docker-connection).
  - In your Azure DevOps project, go to Project Settings (gear icon at the bottom left).
  - Select Service connections under the Pipelines section.
  - Click New service connection:Docker Registry Connection:
       - Choose Docker Registry $\rightarrow$ select your registry type (Docker Hub or Azure Container Registry) $\rightarrow$ name it my-docker-connection $\rightarrow$ authenticate and save.
       - Azure Resource Manager Connection: Choose Azure Resource Manager $\rightarrow$ select Service principal (automatic) $\rightarrow$ choose your Azure Subscription and Resource Group (rg1) $\rightarrow$ name it my-azure-connection $\rightarrow$ save.

### Step 3: Create and Configure the Pipeline
In the left sidebar of Azure DevOps, click Pipelines $\rightarrow$ Pipelines.
Click New pipeline (or Create Pipeline).

Select where your code is stored:

Select Azure Repos Git if you pushed code to Azure Repos.

Select GitHub if your code is hosted on GitHub (you will be prompted to authorize Azure Pipelines).

Select your repository.

In the Configure your pipeline step, select Existing Azure Pipelines YAML file.

Select the Branch (main) and enter the Path to your YAML file (e.g., /01-Project-DeployToAKS-Cluster/azure-pipelines.yml).

Click Continue

### Step 4: Define Pipeline Variables (if required)
Your script references $(DOCKER_USERNAME) in the Kustomize update step:
kustomize edit set image PROJECT/IMAGE=$(DOCKER_USERNAME)/$(imageRepository):$(Build.SourceVersion)

On the pipeline review screen, click Variables.

Click New variable.

Name: DOCKER_USERNAME

Value: Your Docker Hub username or registry namespace

Click Save.

### Step 5: Run and Monitor the Pipeline
Click Run at the top right to start the execution.

Click on the active run to view execution progress:

Build Stage: Builds your Docker image using **/Dockerfile and pushes it to your registry.

Deploy Stage: Downloads code, installs Kustomize, updates the image tag with your build commit SHA, compiles manifests, and deploys to your Azure Kubernetes Service (myAKSCluster).
