#memo
Append citation's file name.
src -> pages -> chat -> Chat.tsx

#Setup
cd frontend
npm install
npm run build
#npm run dev
cd ../
#\stard.cmd


az logout --username shimizuyt@fortience.com
az logout --username shimizuyt@qunie.com
az logout

az login --tenant afb052b9-e6c3-4481-b796-848eb9ede5f1
az account list --output table
az account set --subscription 2fbe88c6-0bee-427e-9309-0f0bce458f15
az account list --output table

#Update Microsoft RAG Apps Template
Move app.py directory
pwsh -v
cd fortience_ai_agent
az webapp up --name asp-app-rag-dev-japanwest-002 --resource-group rg-rag-dev-all-001 --runtime "PYTHON:3.11" --sku B2


#Create New RAG Apps
Move app.py directory
pwsh -v
cd fortience_ai_agent

1.Create env.json
Get-Content .env | ForEach-Object {
     if ($_ -match "(?<name>[A-Z_]+)=(?<value>.*)") {
         [PSCustomObject]@{
             name = $matches["name"]
             value = $matches["value"]
             slotSetting = $false  
         }  
    }  
} | ConvertTo-Json | Out-File -FilePath env.json
2. Deploy
az appservice plan create --name asp-app-rag-dev-japanwest-200 --resource-group rg-rag-dev-all-001 --location japanwest --sku B3 --is-linux
az webapp up --runtime PYTHON:3.11 --sku B3 --name app-rag-dev-japanwest-200 --plan asp-app-rag-dev-japanwest-200 --resource-group rg-rag-dev-all-001 --location japanwest --subscription 2fbe88c6-0bee-427e-9309-0f0bce458f15

3.Set config
az webapp config set --startup-file "python3 -m gunicorn app:app" --name app-rag-dev-japanwest-200
az webapp config appsettings set -g rg-rag-dev-all-001 -n app-rag-dev-japanwest-200 --settings WEBSITE_WEBDEPLOY_USE_SCM=false
az webapp config appsettings set -g rg-rag-dev-all-001 -n app-rag-dev-japanwest-200 --settings "@env.json"

#Update RAG Apps
az webapp up --runtime PYTHON:3.11 --sku B3 --name app-rag-dev-japanwest-200 --resource-group rg-rag-dev-all-001
az webapp config set --startup-file "python3 -m gunicorn app:app" --name app-rag-dev-japanwest-200

#Logging
az webapp log deployment show --resource-group rg-rag-dev-all-001 --name app-rag-dev-japanwest-200


#References
sample-app-aoai-chatGPT
https://github.com/microsoft/sample-app-aoai-chatGPT

