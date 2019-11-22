# Lab 2

## Overview
Introduction to developing using an IoT Edge device and interacting with Microsoft's Azure Services. This session is to get he attendees up to speed with the process of interacting with more complex hardware and some basics around Azure and AI / Cognitive services.

# Agenda
| Time | Topic |
|-----|-----|
|8:30 | Registration and welcome
|9:00  to 13:00 | Hands on labs
|13:00 to 13:30 | Lunch
|13:30 to 16:15 | More hands on labs
|16:15 to 16:30 | Wrap up / demos / feedback


## Hands on labs:
- [Requirements](#requirements) 
- [Labs](#labs)

## Requirements
To install and configure your system you need the following:
 - [VSCode](https://code.visualstudio.com/Download)
    - [Azure IoT Tools](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.azure-iot-tools)
 - [Docker](https://www.docker.com/products/docker-desktop)
 - Azure Subscription
 - [Putty](https://putty.org)

## Labs
Step one, setup your Raspberry Pi as per instructions by Allan.

### Create a IoT Hub instance
1. Login to your Azure Portal and create a resource group
2. Create a new IoT Hub
![](.images/IoTHub.png)
Follow the steps, by selecting the subscription and giving it a unique name. On the next blade, under "Pricing and scale tier" select "F1: Free tier" and create your new IoT Hub
3. Create a new Azure Container Registry (ACR)
![](.images/acr.png)
Take note to **Enable** the Admin user and select **Basic** pricing SKU
4. When the ACR has completed, navigate to it and then select the **Access keys** blade and take note of the login server, admin user and the password

### Create the computer vision model
1. Log into [Computer Vision](https://www.customvision.ai/) site with the same credentials as your Azure account
2. Create a new project setting the values accordingly

|Property|Value|
|----|----|
|Name | Enter a name for your project
|Resource | Select **create new** and create a new resurce in your Azure account putting it in the same resource group as you IoT hub |
|Project Type | Classification
|Classification Type | Multiclass ( Single tag per image)
|Domain | General (compact)
|Export Capability | Basic platforms

3. When the project is created, add the following **Tags** by selecting the "Plus" on the left hand side of the "Train Images" page:
   - Reverse
   - Forward
   - Left
   - Right
   - Stop
4. Make direction instructions with drawn cards or hand signs and take pictures of it to indicate movement of the bot and upload them by selecting the  **Add Images** button and tag then accordingly. 
_Note you need at least 5 images for each tag._
5. When you have sufficient images for each of the actions, select **Train** and perform a **Quick Train**
6. On completion, evaluate the results. At this stage you can also perform a "Quick test" by uploading a picture that was not used in the training set, and see if it evaluates as expected
7. Select **Export** and select to export a **Dockerfile**. When prompted select "ARM (Raspberry PI)" as the version and click **Export** and then **Download**
8. Extract the downloaded file into the **ImageClassifierService** folder under the code path  

### Deploy IoT Edge modules
1. Download the supplied code and open it in VSCode
2. The **.env** file and fill in the values accordingly:

|Property|Value|
|----|----|
|CONTAINER_REGISTRY_ADDRESS | Login Server Name|
|CONTAINER_REGISTRY_USERNAME | Admin user name|
|CONTAINER_REGISTRY_PASSWORD | Password |

3. _TODO @Allan : Make any additional changes and settings_
4. Right click on the "deployment.template.json" file and select **Build and Push IoT Edge Solution**
5. Grab some coffee
