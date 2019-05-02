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
             
     **Problem Statement:** <br />

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

   * Setting up the environment <br />
   
                  cd ~/Desktop
                  mkdir 266Project
                  virtualenv -p /usr/bin/python3
                  virtualenv -p /usr/bin/python3 .
                  source ./bin/activate
                  sudo apt install python3-dev
                  pip install azure-cli

   * Login to the Azure account: <br />
   
		   az login
		  
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-04-30%2023-25-47.png)

   * Create a resource group ‘266Project’ in South Central US: <br />
   
 		   az group create --name 266project --location southcentralus
		   
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-04-30%2023-30-28.png)

   * Create a standard storage account within this resource group ‘266Projectstorage’ in South Central US: <br />
 		   
		   az storage account create --name 266projectstorage --resource-group 266project --location        
		   southcentralus --kind Storage --sku Standard_LRS
		   
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-04-30%2023-34-16.png)
   
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-04-30%2023-34-25.png)



   * Create a container ‘photos’ within this storage account to transfer pics coming in from the cameras: <br />
		   
		   az storage container create --name photos266 --account-name cmpe266storage
		   
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-04-30%2023-41-15.png)
		   

   * Create an IOT hub ‘266hub’ which will connect to the cameras placed in the Arctic in the free tier F1: <br />
		  
		   az iot hub create --name 266hub --resource-group 266project --location southcentralus --sku F1
		   
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-04-30%2023-44-16.png)
		   
 
    * Get the connection string for the IOT hub using the following command: <br />
 		
		   az iot hub show-connection-string --name 266hub
   
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-04-30%2023-44-50.png)
		   

    * Initialise a NodeJS app within the project directory: <br />
		
		   npm init -y
		  
    * Install Azure IOT hub modules to transfer data and images from the cameras to the hub: <br/>
    
		   npm install azure-iothub --save
 		   npm install azure-iot-device azure-iot-device-mqtt --save
		   
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-04-30%2023-47-37.png)

    * Create a file devices.json in the directory and add the content as shown in the Github repository. This file     
      defines the cameras deployed and their longitude and lattitude location. There is a missing key parameter 
      to connect to the IOT hub.
      
    * Create a file deploy.js within the directory and add the content as shown in the Github repository. This file       
      creates a new file cameras.json which also has a key for each camera to connect to the IOT hub using the 
      connection string generated earlier. Run this file: <br />
		
		   node deploy.js
		   
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-04-30%2023-56-20.png)

     * Upload a test image from the photos folder to the IOT hub by running test.js: <br />
 	   
	           node test.js
		   
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-22-36.png)

     * Verify that the blob was received through Azure UI within the photos container created earlier: <br />

   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-23-54.png)
   
     * Create a new resource in Azure UI for a New Stream Analytics Job which will receive live data from the 10 
       Cameras: <br />
       
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-25-13.png)

     * Check if the deployment of the job succeeded: <br />
     
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-25-31.png)

     * To set the IoT hub as its input where the cameras send data, go to its input tab and add the IoT hub created earlier:          <br />
     
   ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-26-06.png)
     
    * Create a file run.js which will transmit events and images to the IoT hub and this is forwarded to the Stream 
      Analytics Job: <br />
		
                   node run.js


     * Go to the query editor within the Stream Analytics Job and enter the query to see if data is being received from the          IoT hub: <br />
     
    ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-29-32.png)


     * To check if an image is transferred from a given camera within 10 seconds which is indicative of a polar bear or any          other animal citing, give the following command. It will reveal the details of the device and the time when the camera        clicked more than once within 10 seconds. Save this query: <br />
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-30-17.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-30-35.png)


     * Create a Function App resource which will be triggered every time the above query is executed and there is 
       a potential polar bear citing. This function app will then trigger the Custom Vision Prediction service to 
       Ascertain whether the animal spotted is indeed a Polar bear as it could be an arctic fox or a walrus as well: <br />
       
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-31-01.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-33-36.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-34-33.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-36-14.png)

     * Within the Function App, create a Webhook + API which will run whenever it receives an HTTP request from  
       the Stream Analytics Job: <br />
       
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-36-44.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-36-51.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-37-25.png)

     * Add Function App as the output to the Stream Analytics job: <br />
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-38-18.png)

     * Change the saved query to save the data into the FunctionOutput created in the previous step and save it: <br />
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-38-51.png)

     * Run run.js to start transmitting data and images to the IoT hub. The images are being transferred from the photos              folder. Start the Stream Analytics job which will accept input data from the IoT hub and invoke the saved quey and            forward the output to the Function app: <br />
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-42-06.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-39-20.png)


     * Go to the Function app to verify if data the function is being invoked: <br />
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-43-19.png)

     * Stop the Stream Analytics Job for now. <br />

     * Create a new resource for Custom Vision Prediction. This service will take an input from the Function app and 
       predict if the animal is spotted is indeed a Polar bear: <br />
       
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-49-16.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-50-36.png)


     * Go to the custom vision official website and create a project within the same resource group: <br />
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-56-55.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-57-02.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2000-57-09.png)


     * Add sample images of polar bears, walruses and arctic foxes to train the model and add their respective 
       tags: <br />
       
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-01-09.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-01-21.png)

     * Click on the Performance tab to do the first iteration and build the model <br />
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-01-30.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-01-47.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-01-52.png)


    * Do a Quick test and upload test images to see if the model is performing as expected: <br />
    
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-07-01.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-07-13.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-07-38.png)


    * After confirming, publish the model to be used further:
    
    ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-08-48.png)
    
    ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-09-02.png)
    
    ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-13-09.png)

    * Create a DB server and DB where the Function app will save the data after confirming with the Custom Vision Prediction         Service if the animal is a Polar bear or no. There will be a isPolarBear boolean attribute which will confirm if the           animal is indeed a Polar bear. The Custom Vision Service returns true if the model can predict with more than 80 percent       certainty that the animal is a polar bear: <br />
    
                   az sql server create --name 266projectdb --resource-group 266project --location southcentralus 
                   --admin-user roopam --admin-password xxxxxx
 	           az sql db create --resource-group 266project --server 266projectdb --name PolarBearDB 
	           --service-objective S1
		   
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-15-40.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-18-37.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-18-42.png)



     * Go to the DB server firewall settings and turn on access to the azure services: <br />
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-20-22.png)
     
     * Login to the database and create a table PolarBears: <br />

    ```
    CREATE TABLE [dbo].[PolarBears]
    (
    [Id] [uniqueidentifier] NOT NULL,
    [CameraId] [nvarchar](16) NULL,
    [Latitude] [real] NULL,
    [Longitude] [real] NULL,
    [Url] [varchar](max) NULL,
    [Timestamp] [datetime] NULL,
    [Probability] [real] NULL,
    [IsPolarBear] [bit] NULL,
    PRIMARY KEY CLUSTERED ([Id] ASC)
    WITH (STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF) ON [PRIMARY]
    )
    ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
    GO

    ALTER TABLE [dbo].[PolarBears] ADD DEFAULT (newid()) FOR [Id]
    GO

    ALTER TABLE [dbo].[PolarBears] ADD DEFAULT (getdate()) FOR [Timestamp]
    GO

   ALTER TABLE [dbo].[PolarBears] ADD DEFAULT ((0)) FOR [IsPolarBear]
   GO
  ```

     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-20-54.png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-23-14.png)
     
     * Go to the Function app and replace the instructions in the index.js file with the code in function.txt file in the            project folder: <br />
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20from%202019-05-01%2001-46-50.png)

      Here predictionUrl and predictionKey come from the Custom Vision Prediction service. Other storage account details and         database details are added as shown above.
      The function app takes an input from the Stream Analytics Job, triggers the Custom Vision Service and uploads the data         into the SQL database with a isPolarBear flag value either 1 or 0 as returned by the Prediction service.

     * Go to the database created and see if it data is coming in from the Function App: <br />
		
		   SELECT * from dbp.PolarBears
		     
     * This data can then be analysed using Microsoft Power BI service. The following screenshots show the various formatting        functionalities that Power BI provides : <br />
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(109).png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(110).png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(111).png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(112).png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(113).png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(114).png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(115).png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(116).png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(117).png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(118).png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(119).png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(120).png)
     
     ![img](https://github.com/acharyarohan/CMPE-266-Team-Project/blob/master/Screenshots/Screenshot%20(121).png)
     
     
     
* Solution for each requirement present in the problem statement? <br />

      1. Microsoft Azure IoT Hub: This can be used to ingest any kind of streaming data via a simulated recording media for            example - cameras. 
      2. Microsoft Azure Storage: Any kind of streaming data can be stored here. 
      3. Microsoft Azure Stream Analytics: This service can be used to process real-time data streams. 
      4. Microsoft Azure Function: This service can be used to process outputs from the Stream Analytics service. 
      5. Microsoft Custom Vision Service: This service can be used to analyze/recognize images. 
      6. Microsoft Power BI: This service can be used to create customized dashboards for data visualization. 
      7. Microsoft Azure SQL Database: This service can be used to store relational data. 


* Public URL to the application: <br />

    * Refer following Github repository to access project code and set up steps: 

      https://github.com/acharyarohan/CMPE-266-Team-Project 


* URL to Github repo : <br />

     https://github.com/acharyarohan/CMPE-266-Team-Project 


