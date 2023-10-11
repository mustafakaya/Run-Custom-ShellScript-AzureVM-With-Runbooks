# Run-Custom-ShellScript-AzureVM-With-Runbooks
This article will guide you through the process of running shell scripts on your Azure Linux VMs directly from your Azure Automation account and then will integrate with Azure Site Recovery  - Recovery Plan to run you custom script as post action. 

![image](https://github.com/mustafakaya/Run-Custom-ShellScript-AzureVM-With-Runbooks/assets/9195953/7fb5aeb2-65ab-40d3-8884-7d7ac498612b)

## 1-	Create ARM template and parameters for Custom Script Extension:
 
 ![image](https://github.com/mustafakaya/Run-Custom-ShellScript-AzureVM-With-Runbooks/assets/9195953/f0ab67cf-e4af-492c-ae49-2c42ed0acdc6)

Example parameters file as below. 

![image](https://github.com/mustafakaya/Run-Custom-ShellScript-AzureVM-With-Runbooks/assets/9195953/55f5ec45-fccc-408c-bfc8-c0d5b8b8e4b4)


Upload your template and parameters file to Storage Account as below. 

![image](https://github.com/mustafakaya/Run-Custom-ShellScript-AzureVM-With-Runbooks/assets/9195953/0b4a9daf-ef76-46a1-855e-18114df6c747)

 
Don’t forget to change the access level as below:

![image](https://github.com/mustafakaya/Run-Custom-ShellScript-AzureVM-With-Runbooks/assets/9195953/e373ddfb-33e7-40ec-94fb-ef5a4e786af0)

 
## 2-	Create System Assigned Managed Identity for your Automation Account

You need an identity object to connect your Azure VM and install an extension from Automation Account.  You can create System Assigned identity and assign required Azure Role.
 
![image](https://github.com/mustafakaya/Run-Custom-ShellScript-AzureVM-With-Runbooks/assets/9195953/e51fbc38-1514-4127-8258-49d829385b88)


## 3- Create runbook with the following PowerShell script:

![image](https://github.com/mustafakaya/Run-Custom-ShellScript-AzureVM-With-Runbooks/assets/9195953/b2e4b522-de93-4f78-8757-9f77744e1cc4)

 
$resourceGroupName="asr-ss-rg"
$templateFile="https://yourstorage.blob.core.windows.net/templates/template.json"
$templateParameterFile="https://yourstorage.blob.core.windows.net/templates/parameters.json"
Connect-AzAccount -Identity 
New-AzResourceGroupDeployment -ResourceGroupName $resourceGroupName  -TemplateUri $templateFile  -TemplateParameterUri $templateParameterFile


## 4-	Prepare your shell script and upload to Storage Account:

![image](https://github.com/mustafakaya/Run-Custom-ShellScript-AzureVM-With-Runbooks/assets/9195953/8a49f83d-d55f-4dca-bc03-dea5d178adf9)


## 5-	Go to Site Recovery Plan in Site Recovery vault and add post failover action as previous created Runbook to proper your virtual machine group:

 ![image](https://github.com/mustafakaya/Run-Custom-ShellScript-AzureVM-With-Runbooks/assets/9195953/7c9efd4b-d693-4b0a-9b76-d41ebe238f37)

 ![image](https://github.com/mustafakaya/Run-Custom-ShellScript-AzureVM-With-Runbooks/assets/9195953/63d494c2-fa24-4ffd-b106-8a65fc5d47a4)

 ![image](https://github.com/mustafakaya/Run-Custom-ShellScript-AzureVM-With-Runbooks/assets/9195953/4bdea734-96cc-4a15-a11a-54dbb643a6d5)

 ![image](https://github.com/mustafakaya/Run-Custom-ShellScript-AzureVM-With-Runbooks/assets/9195953/909d71a4-95fc-47b5-859a-a081492c8076)




 
 
 

