
# ASP.NET Azure App
https://learn.microsoft.com/en-us/azure/app-service/quickstart-dotnetcore?tabs=net80&pivots=development-environment-cli

## Create App Locally
appName=pnrdevopswebapp
echo $appName
dotnet new webapp -n $appName --framework net8.0
cd $appName

dotnet run --urls=https://localhost:5001/

## Publish your web app
az account clear
az config set core.enable_broker_on_windows=false
az login --tenant pietronromanolive.onmicrosoft.com

## Resource group will be created if doesn't exist
rg="rg-devops"
echo $rg

az webapp up --sku F1 --name $appName --os-type linux --location westeurope --resource-group $rg 

## RESULTS:
Status: Site started successfully. Time: 206(s)
You can launch the app at http://pnrdevopswebapp.azurewebsites.net
Setting 'az webapp up' default arguments for current directory. Manage defaults with 'az configure --scope local'
--resource-group/-g default: rg-devops
--sku default: F1
--plan/-p default: pietronromano_asp_2782
--location/-l default: westeurope
--name/-n default: pnrdevopswebapp
{
  "URL": "http://pnrdevopswebapp.azurewebsites.net",
  "appserviceplan": "pietronromano_asp_2782",
  "location": "westeurope",
  "name": "pnrdevopswebapp",
  "os": "Linux",
  "resourcegroup": "rg-devops",
  "runtime_version": "dotnetcore|8.0",
  "runtime_version_detected": "8.0",
  "sku": "FREE",
  "src_path": "C:\\dev\\devops\\pnrdevopswebapp"
}

## You can launch the app at http://<app-name>.azurewebsites.net

## Alter index.cshtml, then redeploy
az webapp up --os-type linux