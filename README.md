### CI-CD_WITH_JENKINS_AND_AZURE_DEVOPS
_This uses Jenkins for continuous integration and Azure DevOps for continuous deployment._

> Due to an already established CI pipeline on Jenkins and the decision to leverage the advanced deployment capabilities of Azure DevOps, this setup hands over the build artifact to Azure DevOps from the Jenkins pipeline.


##

<img src="https://github.com/user-attachments/assets/da0a17e8-0d8f-4dd5-9a10-bd7f20ff0449" alt="CI/CD WITH JENKINS AND AZ-DEVOPS-ARCHI" style="height: 350px; width:600;"/> 

##

<img src="https://github.com/user-attachments/assets/12f22a6d-7464-42c3-845e-09cfea14aa08" alt="Stage breakdown" style="height: 100px; width:200;"/>

<table>
  <tr>
    <td>
      <img src="https://github.com/user-attachments/assets/0e5341c2-9429-4efb-8cd5-299ff8b6f7fc" alt="SETUP STAGE" style="height: 400px; width:1400px;"/> 
    </td>
    <td>
      
__Create Azure DevOps Project__: Initiate the release pipeline setup by creating an Azure DevOps organization from the Azure portal, then make a private project in the organization.

__Personal Access Token__: From user's setting on the project page, create a PAT with full access permission granted.

__Self-Hosted Linux Agent__: Handles deployment processes; pulling archive, unpacking, setting env variables, dependencies etc and finally deploying to Azure Web App. Create a Linux VM, Download and install Linux agent on the VM, use above PAT token to register the agent as 'Default' agent pool, and run the agent to listen for jobs from Azure DevOps.

__Jenkins__: CI/CD server for building and archiving the nodejs code and files; add the task as a 'freestyle project', configure the source code repository with a 'jenkins' branch, add shell command 'zip -r archive.zip node_modules package.json server.js' to the 'build step action' and add 'archive.zip' to the 'postbuild action' section.
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img src="https://github.com/user-attachments/assets/d7fe3f29-6c41-410f-ab9b-f64b6c1da8b1" alt="BUILD STAGE" style="height: 400px; width:650px;"/>
    </td>
    <td>
      
__Pull Git Repo__: Fork the provided git repo to own repo that can be used in the Jenkins pipeline. 
      
__Build & Package App__: Trigger pipeline from Jenkins interface to build and archive application. Archive artifact to be used in the release pipeline on azure devops.  
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img src="https://github.com/user-attachments/assets/9237ca5a-a052-46ca-8411-bb46f505d69f" alt="RELEASE STAGE" style="height: 400px; width:2000px;"/>
    </td>
    <td>
      
__Service Principal__: Create 'Azure Resource Manager' service connection type using 'service principal (manual)' as the authentication type. The following parameters are required: Subscription Id, Subscription Name, Service Principal Id, Service principal key and Tenant Id, which can be retrieved by running the command 'Get-AzSubscription' from Azure Cloud shell. 

__Jenkins Connection__: Configure azure devops to establish connections to jenkins server. Create a 'Jenkins' service connection type, and input parameters: Jenkins URL, username, password, and service connection name. 

__Deploy__: Initiate release pipeline; Create empty release job from the Azure Devops project, select 'jenkins artifact' and the jenkins connection type created earlier, in the agent pool section, select the 'default' agent created earlier for self-hosted agent, then add a task and 'select azure web app'. Configure Azure web app with the parameters: Display Name, Subscription connection(use previously created service principal), App type(Web App on Linux), then App name.  
Save and initiate release to deploy on Azure Web App. 
    </td>
  </tr>
</table>

