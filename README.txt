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

#Deploy
Move app.py directory
pwsh -v
cd fortience_ai_agent
Compress-Archive -Path * -DestinationPath ..\fortience-ai-agent.zip -Force
# or
# Get-ChildItem -Recurse -File | Where-Object { $_.FullName -notlike "*\.git\*" -and $_.FullName -notlike "*node_modules*" -and $_.FullName -notlike "*\.venv\*"} | Compress-Archive -DestinationPath ..\fortience-ai-agent.zip -Force
az webapp deployment source config-zip --resource-group rg-rag-dev-all-001 --name app-rag-dev-japanwest-002 --src ..\fortience-ai-agent.zip

#Logging
az webapp log deployment show --resource-group rg-rag-dev-all-001 --name app-rag-dev-japanwest-002


#References
sample-app-aoai-chatGPT
https://github.com/microsoft/sample-app-aoai-chatGPT

