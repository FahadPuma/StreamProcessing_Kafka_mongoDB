# **StreamProcessing_Kafka_mongoDB**
A basic ETL pipeline to receive live stream data generated and collected over Apache Kafka and stored in mongoDB for further processing and reporting.

### **Use Case:**
To check the quality of a driver in terms of following rules. The vital information like the vehicle location, speed is gathered by the GPS which is fitted in the vehicle and transmitted in near-real-time to a centralized server maintained in the cloud network over MQTT protocol. This information is then available for the authorized users in real time and each licensed vehicle owner can access the data in cloud using a web portal anytime anywhere. This system thus provides an accurate positioning of the vehicle, speed, driver's condition and provides an intelligent monitoring of the vehicle remotely.

#### Below is a list of basic requirement and the corresponding steps to:

1)	Capturing the real time truck movement data from the sensors fitted in the trucks
    This will be simulated by creating a dictionary of data for each of the trucks with id, License, DriverId, name, speed etc.
2)	Moving the running truck data over MQTT protocol to a centralized location
3)	Moving data from centralized location to messaging store for intermittent storage(mongoDB)
4)	Preprocessing of the data received from the trucks for quality checks and for other required transformations(mongoDB)
5)	Doing the processing of data to identify the drivers exceeding the speed limits. Moving the data separately into another table whenever spped>100
6)	Providing a way to maintain the count of over speeding incidents over the period of time, on particular routes, for particular trucks etc.
7) Querying the mongoDB database to extract the aggregated information for oversppeding vehicles and drivers.

### <ins> **Solution Architecture:** </ins>
#### **Architecture Diagram:**
![Picture 1](https://user-images.githubusercontent.com/87992010/212901708-8d57b665-7c8b-45ca-952d-0456511e17c5.png)
#### Step 1:
Simulation of truck data and sending it over MQTT protocol to mosquito broker
![Picture 2](https://user-images.githubusercontent.com/87992010/212906636-a4b5eb7b-6ad6-4977-9f7b-ccb2eeb26890.png)
#### Step 2:
Data transfer program from Mosquito broker to Kafka Topic and a raw data storage in kafka
![Picture 3](https://user-images.githubusercontent.com/87992010/212907279-3c1cb0b9-136b-4ed9-8c86-867f83ff1371.png)
#### Step 3:
Data preprocessing / filtering program for identifying over speeding cases(>100) and sending it to another mongoDB table
![Picture 4](https://user-images.githubusercontent.com/87992010/212907506-4edf22ca-bc00-4782-aac8-c94f9880b564.png)
#### Step 4:
Creating a function keep statistics about over speeding cases over the period of time, for different routes, for different Drivers etc. 
![Picture 5](https://user-images.githubusercontent.com/87992010/212908069-a7504b82-1d37-46b7-a922-24aa45f41d41.png)
