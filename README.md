### CI-CD_WITH_JENKINS_AND_AZURE_DEVOPS
_This uses Jenkins for continuous integration and Azure DevOps for continuous deployment._

> Due to an already established CI pipeline on Jenkins and the decision to leverage the advanced deployment capabilities of Azure DevOps, this setup hands over the build artifact to Azure DevOps from the Jenkins pipeline.
##

<img src="https://github.com/user-attachments/assets/da0a17e8-0d8f-4dd5-9a10-bd7f20ff0449" alt="CI/CD WITH JENKINS AND AZ-DEVOPS-ARCHI" style="height: 350px; width:600;"/> 

##

<img src="https://github.com/user-attachments/assets/0e5341c2-9429-4efb-8cd5-299ff8b6f7fc" alt="SETUP STAGE" style="height: 350px; width:600;"/> 

__Create Azure DevOps Project__: Initiate the release pipeline by creating an Azure DevOps organization from the Azure portal, then make a private project in the organization.

__Personal Access Token__: From the user's setting on the project page, create a PAT with full access permission granted.

__Self-Hosted Agent__

##

<img src="https://github.com/user-attachments/assets/d7fe3f29-6c41-410f-ab9b-f64b6c1da8b1" alt="BUILD STAGE" style="height: 350px; width:600;"/>

##

<img src="https://github.com/user-attachments/assets/9237ca5a-a052-46ca-8411-bb46f505d69f" alt="RELEASE STAGE" style="height: 350px; width:600;"/>

