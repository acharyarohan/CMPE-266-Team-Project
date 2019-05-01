# CMPE-266-Team-Project

## CMPE 266 Big Data Project - Spring 2019

![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/sjsu_logo.png)

* University Name : San Jose State University 

* Course: Big Data Engineering and Analytics

* Professor: [Sanjay Garje](http://www.sjsu.edu/people/sanjay.garje/) 

* Students : <br />
   [Roopam Rajvanshi](https://www.linkedin.com/in/roopamrajvanshi/) <br />
   [Rohan Acharya](https://www.linkedin.com/in/acharyarohan/)  


## Architecture Diagram: 

![img](https://user-images.githubusercontent.com/33761930/56635961-278a4000-661c-11e9-9a4c-eafb0dc8676e.JPG)

* What is the project idea /What the Big Data application does?
             
     **Problem Statement:** 


> A senior climate scientist in the Arctic is worried about the extinction of polar bears in the region. He has placed hundreds of motion-activated cameras at marked location throughout the region. He now wants to devise an automated system that can process data from these cameras in real time and can display some sort of notification when a bear is clicked. He would also need a very fast ‘over-the-cloud’ service to recognize bears in these photographs so that he and his team can take appropriate actions. <br />
                              The project idea deals with building a big-data application using Microsoft Azure and Microsoft Cognitive Services. Data in the form of photos will be streamed and processed real-time and will be analyzed via an image recognition service. The results will done by presented in a customized dashboard using data from a fully deployed database. Therefore, the application follows the entire flow of collecting, classifying and visualizing big data in the real world. 
                            

* What are the technologies used? <br />
1. Microsoft Azure IoT Hub 
2. Microsoft Azure Storage
3. Microsoft Azure Stream Analytics
4. Microsoft Azure Functions
5. Microsoft Custom Vision Service
6. Microsoft Power BI
7. Microsoft Azure SQL Database 

* Solution for each requirement present in the problem statement? <br />

1. Microsoft Azure IoT Hub: This can be used to ingest any kind of streaming data via a simulated recording media for example - cameras. 
2. Microsoft Azure Storage: Any kind of streaming data can be stored here. 
3. Microsoft Azure Stream Analytics: This service can be used to process real-time data streams. 
4. Microsoft Azure Function: This service can be used to process outputs from the Stream Analytics service. 
5. Microsoft Custom Vision Service: This service can be used to analyze/recognize images. 
6. Microsoft Power BI: This service can be used to create customized dashboards for data visualization. 
7. Microsoft Azure SQL Database: This service can be used to store relational data. 

* Sample Demo Screenshots: 

   * Setting up the environment
         1. cd ~/Desktop
         2. mkdir 266Project
         3. virtualenv -p /usr/bin/python3
         4. virtualenv -p /usr/bin/python3 .
         5. source ./bin/activate
         6. sudo apt install python3-dev
         7. pip install azure-cli

   * Login to the Azure account: <br />
		   1. az login

   * Create a resource group ‘266Project’ in South Central US: <br />
 		   1. az group create --name 266project --location southcentralus

   * Create a standard storage account within this resource group ‘266Projectstorage’ in South Central US: <br />
 		   1. az storage account create --name 266projectstorage --resource-group 266project --location        
		   2. southcentralus --kind Storage --sku Standard_LRS


   * Create a container ‘photos’ within this storage account to transfer pics coming in from the cameras: <br />
		   1. az storage container create --name photos266 --account-name cmpe266storage

   * Create an IOT hub ‘266hub’ which will connect to the cameras placed in the Arctic in the free tier F1: <br />
		   1. az iot hub create --name 266hub --resource-group 266project --location southcentralus --sku F1


     7.    Get the connection string for the IOT hub using the following command:
 		az iot hub show-connection-string --name 266hub

     8.    Initialise a NodeJS app within the project directory:
		npm init -y
     9.    Install Azure IOT hub modules to transfer data and images from the cameras to the hub:
		npm install azure-iothub --save
 		npm install azure-iot-device azure-iot-device-mqtt --save

     8.  Create a file devices.json in the directory and add the content as shown in the Github repository. This file     
           defines the cameras deployed and their longitude and lattitude location. There is a missing key parameter 
           to connect to the IOT hub.
     9.    Create a file deploy.js within the directory and add the content as shown in the Github repository. This file       
	creates a new file cameras.json which also has a key for each camera to connect to the IOT hub using the 
	connection string generated earlier. Run this file:
		node deploy.js

     10.   Upload a test image from the photos folder to the IOT hub by running test.js:
 		node test.js

   





  11.    Verify that the blob was received through Azure UI within the photos container created earlier:


   12.    Create a new resource in Azure UI for a New Stream Analytics Job which will receive live data from the 10 
	Cameras:

     





13.    Check if the deployment of the job succeeded:

14.    To set the IoT hub as its input where the cameras send data, go to its input tab and add the IoT hub created earlier:


15.    Create a file run.js which will transmit events and images to the IoT hub and this is forwarded to the Stream 
          Analytics Job:
		node run.js


16.    Go to the query editor within the Stream Analytics Job and enter the query to see if data is being received from the IoT hub:


17.    To check if an image is transferred from a given camera within 10 seconds which is indicative of a polar bear or any other animal citing, give the following command. It will reveal the details of the device and the time when the camera clicked more than once within 10 seconds. Save this query:






18.    Create a Function App resource which will be triggered every time the above query is executed and there is 
          a potential polar bear citing. This function app will then trigger the Custom Vision Prediction service to 
          Ascertain whether the animal spotted is indeed a Polar bear as it could be an arctic fox or a walrus as well:




19.    Within the Function App, create a Webhook + API which will run whenever it receives an HTTP request from  
          from the Stream Analytics Job:



20.    Add Function App as the output to the Stream Analytics job: 

21.    Change the saved query to save the data into the FunctionOutput:

13.    Check if the deployment of the job succeeded:

13.    Check if the deployment of the job succeeded:

13.    Check if the deployment of the job succeeded:


* Public URL to the application: <br />

    * Refer following Github repository to access project code and set up steps: 

      https://github.com/acharyarohan/CMPE-266-Team-Project 

* Test Account Credentials:  <br />

    * Microsoft Azure Portal Credentials are as follows-

      > Username : rrajvanshi1947@gmail.com <br />
        Password : 

* URL to Github repo : <br />

     https://github.com/acharyarohan/CMPE-266-Team-Project 


