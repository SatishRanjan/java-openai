# OpenAI with Java
The project demonstrate the integration with Azure OpenAI text-davinci-003 model, Azure Storage Queue using JAVA. The purpose of this repository is to provide a reference point with the Azure OpenAI "text-davinci-003" model serving as an example POC to build a java WebJob or for an independent local run test.

## Demo App Architecture

![alternativetext](/demoapp-arch.png)

## Pre-requisite
- Azure Open AI service created and text-davinci-003 model deployed
- Have a Azure Storage source and destination queues created
- Acquire the below config information and have the needed environment variables setup

## How to Run
- Install platform specific Java 17 onwards, e.g. for windows https://learn.microsoft.com/en-us/java/openjdk/download
- Make sure JAVA_HOME environment variable is configured
- Install mvn(maven) https://maven.apache.org/download.cgi

## Build
- Clone the repo locally
- Navigate to the cloned directory
- run "mvn compile" then "mvn package"
- Running "mvn package" would generate the jar file "openapi-javaapp-1.0.0.jar" under \target directory
## Running jar locally
- Have these environment variable configured that contains the configuration for the azure open AI, azure storage queue
  -  AZURE_STORAGE_CONNECTION_STRING
  -  AZURE_STORAGE_SOURCE_QUEUE_NAME
  -  AZURE_STORAGE_DESTINATION_QUEUE_NAME
  -  AZURE_OPEN_API_KEY
  -  AZURE_OPEN_API_ENDPOINT
  -  AZURE_OPEN_API_MODEL_DEPLOYMENT_NAME
- Run the jar using "**java -jar target\openapi-javaapp-1.0.0.jar**", if there's no error and run completes and exits, then the jar content is all good to be deployed as webjob in azure.
- To see the content of the jar file run "**jar -tf target\openapi-javaapp-1.0.0.jar**" or extract the jar content locally

## Running As WebJob in Azure
Currently EastUSEUAP2 has the code deployed that enables running webjobs on Linux. 
 - Create a Java Linux container webapp, please make sure the container, custom or blessed image based have Java 17 + in it, JAVA_HOME environment variables configured, and WEBSITES_ENABLE_APP_SERVICE_STORAGE environment variable set to true for the web app
 - Have the above mentioned environment varialbes configured as app settings
 - Please zip these files "**openai-java-webjob-start.sh**", "**settings.jo**b" and "**openapi-javaapp-1.0.0.jar**". And deploy the zip file as  continuous webjob, either by zip deployment or by calling webjob PUT API, details here https://github.com/projectkudu/kudu/wiki/WebJobs-API
   
