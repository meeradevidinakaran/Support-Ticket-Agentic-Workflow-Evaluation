# Langflow Set up 
For this scenario we have created a langflow container on docker desktop.
 
 Pre-requisite Setup
Install Docker Desktop - Docker Desktop is a free application that lets you run Docker containers on your computer. 
Visit the official Docker Desktop download page: https://www.docker.com/products/docker-desktop/ Download OS specific Version, Install and restart to see docker instance running. Use command prompt to ensure docker isntallation is successful - "docker --version"
langflow on docker With Docker running, use this single command to download and start Langflow: "docker run -it -p 7860:7860 langflowai/langflow:latest" Once Completed,Open your web browser and go to: http://localhost:7860

Steps to get started on Langflow.
Start Creating workflows on langflow local instance. Use a Chat Input and connect it to an Agent. Within each agent Connect to the Open AI using a valid API Key and select preferred LLM models. Provide agent instructions in System prompts.

# Langfuse Set up
Create a Langfuse account- Go to https://cloud.langfuse.com
Sign up (free tier, no credit card).Once logged in, click "+ New Project" and provide a desired name to it.
Once project is created , go to the settings page and select the **API keys** Tab you will see three Values - Secret Key , Public Key and Host. Copy them for further set up.
Open Evaluators tab - Select couple of LLM as judge from existing templates and hit execute to activate them. You can also create a new one with custom prompt and model by clicking on the "Set Up Evaluator" Button on top right.

# Connect Langflow to Langfuse- API key Set up
Use the below commands on a windows powershell
__docker run -d `
  --name langflow-container `
  -p 7860:7860 `
  -e LANGFUSE_PUBLIC_KEY=your_public_key `
  -e LANGFUSE_SECRET_KEY=your_secret_key `
  -e LANGFUSE_HOST=https://cloud.langfuse.com `
  -e LANGFLOW_TRACING_ENABLED=true `
  -v C:\langflow\data:/app/langflow/data `
  your langflow image name on docker_
Hit Enter and you will see a new container space is created on docker , you can remove any existing container by using _docker rm yourcontainer_.
Verify if API keys are set using >> _docker exec -it langflow-container env | findstr LANGFUSE_

Once done Open Langflow create/ import a workflow and test in playground with a single user prompt. Parallely open Langfuse and check for traces and evaluators.
