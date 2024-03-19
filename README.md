# REST Booking API Testing with Postman & Newman
This project aims to automate the testing of a REST booking API using Postman and Newman. By automating the testing process, I ensure consistent and reliable validation of the API endpoints, reducing manual effort and enabling faster feedback on changes.
# Features
•	Comprehensive API testing suite covering various HTTP methods including GET, POST, PUT, PATCH, and DELETE.<br/>
•	Requests with different configurations such as request bodies, pre-request scripts, and tests to ensure comprehensive API endpoint validation.<br/>
•	Easy-to-use Postman collections for executing tests locally or integrating into continuous integration pipelines.<br/>
•	Detailed test scripts to validate responses and ensure API functionality meets requirements.<br/>
•	Modularized structure for easy maintenance and scalability of test suites.
# API Documentation
https://documenter.getpostman.com/view/33497213/2sA2xpS9Em
# Technology Used
1.	**Postman:** Used for creating and managing API requests and collections.
2.	**Newman:** Command-line collection runner for Postman, allowing for execution in CI/CD pipelines or terminal environments.
# Prerequisite
Before running the tests, ensure you have the following installed:</br>
**•	Postman:** <a href="https://www.postman.com/downloads/">Download and install Postman</a> on your machine.</br>
**•	Node.js:** <a href="https://nodejs.org/en">Install Node.js</a> to be able to run Newman.</br>
**•	Newman** Html Report Library
# Installation
  **1. Import the Postman collection:** </br>
    • Open Postman </br>
    •	Click on the Import button</br>
    • Select the file from the repository</br>
  **2. Import the Postman environment:** </br>
    •	In Postman, click on the gear icon in the top right corner.</br>
    •	Select Import and choose the file.</br>
  **3. Newman and Report Installation Process:** <br/>
    •	Newman Install Command</br>
       `npm install -g newman` <br/>
    •	Newman Html Report Install Command:<br/>
       `npm install -g newman-reporter-htmlextra`
# Usage
  **1. Select Environment:** <br/>
      In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.<br/>
  **2. Run Collection:** <br/>
      Select the imported collection from the Collections sidebar.<br/>
      Click on the Runner button to open the collection runner.<br/>
      Select the desired environment.<br/>
      Click Start Test to run the collection.<br/>
  **3. View Results:** <br/>
      Once the tests are complete, view the results in the Runner tab.<br/>
      Detailed test results can be viewed for each request.<br/>
# Testing
  ### 1. Create Booking.
  #### URL: https://restful-booker.herokuapp.com/booking/
  #### METHOD: POST
  #### Pre-request Script:
```
// Generate Random Values Then Set That into Environment
pm.environment.set("fName", pm.variables.replaceIn("{{$randomNamePrefix}} {{$randomFirstName}}"))
pm.environment.set("lName", pm.variables.replaceIn("{{$randomLastName}}"))
pm.environment.set("tPrice", pm.variables.replaceIn("{{$randomInt}}"))
pm.environment.set("dPaid", pm.variables.replaceIn("{{$randomBoolean}}"))

const date = require('moment')
// FORMAT AS YYYY-MM-DD THEN SET THAT TO ENVIRONMENT
const today = date().format('YYYY-MM-DD')
pm.environment.set("ciDate", today)

// 2 DAYS FORWARD FROM CURRENT THEN SET THAT TO ENVIRONMENT
const future = date().add(2, 'days').format('YYYY-MM-DD')
pm.environment.set("coDate", future)

// RANDOMLY SELECT MEAL THEN SET IT TO ENVIRONMENT
const meals = ["Breakfast", "Lunch", "Brunch", "Dinner"]
const selected = meals[Math.floor(Math.random() * meals.length)]
pm.environment.set("extraNeeds", selected)
```
#### Request Body:
```
{
"firstname" : "{{fName}}",
"lastname" : "{{lName}}",
"totalprice" : {{tPrice}},
"depositpaid" : {{dPaid}},
"bookingdates" : {
"checkin" : "{{ciDate}}",
"checkout" : "{{coDate}}"
},
"additionalneeds" : "{{extraNeeds}}"
}
```
#### Response Body:
```
{
    "bookingid": 3078,
    "booking": {
        "firstname": "Ms. Hassan",
        "lastname": "Crona",
        "totalprice": 619,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2024-03-19",
            "checkout": "2024-03-21"
        },
        "additionalneeds": "Dinner"
    }
}
```
### 2. Read After Create Booking.
#### URL: https://restful-booker.herokuapp.com/booking/3078
#### METHOD: GET
#### Response Body:
```
{
    "firstname": "Ms. Hassan",
    "lastname": "Crona",
    "totalprice": 619,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-03-19",
        "checkout": "2024-03-21"
    },
    "additionalneeds": "Dinner"
}
```
### 3. Create A Token For Authentication.
#### URL: https://restful-booker.herokuapp.com/auth
#### METHOD: POST
#### Request Body:
```
{
"username": "admin",
"password": "password123"
}
```
#### Response Body:
```
{
    "token": "7bf209311ab4740"
}
```
### 4. Modify A Booking.
#### URL: https://restful-booker.herokuapp.com/booking/3078
#### METHOD: PUT
#### Pre-request Script:
```
// GENERATE RANDOM VALUES THEN SET THAT into ENVIRONMENT
pm.environment.set("ufName", pm.variables.replaceIn("{{$randomNamePrefix}} {{$randomFirstName}}"))
pm.environment.set("ulName", pm.variables.replaceIn("{{$randomLastName}}"))
pm.environment.set("utPrice", pm.variables.replaceIn("{{$randomInt}}"))
pm.environment.set("udPaid", pm.variables.replaceIn("{{$randomBoolean}}"))

// GET THE CURRENT DATE
const date = require('moment')

// FORMAT AS YYYY-MM-DD THEN SET THAT TO ENVIRONMENT
const today = date().add(1, 'd').format('YYYY-MM-DD')
pm.environment.set("uciDate", today)

// 2 DAYS FORWARD FROM CURRENT THEN SET THAT TO ENVIRONMENT
const future = date().add(3, 'd').format('YYYY-MM-DD')
pm.environment.set("ucoDate", future)

// RANDOMLY SELECT MEAL THEN SET IT TO ENVIRONMENT
const meals = ["Breakfast", "Lunch", "Brunch", "Dinner"]
const selected = meals[Math.floor(Math.random() * meals.length)]
pm.environment.set("uextraNeeds", selected)
```
#### Request Body:
```
{
    "firstname": "{{ufName}}",
    "lastname": "{{ulName}}",
    "totalprice": {{utPrice}},
    "depositpaid": {{udPaid}},
    "bookingdates": {
        "checkin": "{{uciDate}}",
        "checkout": "{{ucoDate}}"
    },
    "additionalneeds": "{{uextraNeeds}}"
}
```
#### Response Body:
```
{
    "firstname": "Mrs. Clovis",
    "lastname": "Ferry",
    "totalprice": 541,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2024-03-20",
        "checkout": "2024-03-22"
    },
    "additionalneeds": "Dinner"
}
```
### 5. Read After Modify Booking
#### URL: https://restful-booker.herokuapp.com/booking/3078
#### METHOD: GET
#### Response Body:
```
{
    "firstname": "Mrs. Clovis",
    "lastname": "Ferry",
    "totalprice": 541,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2024-03-20",
        "checkout": "2024-03-22"
    },
    "additionalneeds": "Dinner"
}
```
### 6. Partially Modify A Booking.
#### URL: https://restful-booker.herokuapp.com/booking/3078
#### METHOD: PATCH
#### Pre-request Script:
```
// GENERATE RANDOM VALUES AND STORE INTO A VARIABLE. PASS THE VARIABLE TO ENVIRONMENT.
var res = pm.variables.replaceIn("{{$randomNamePrefix}} {{$randomFirstName}}")
pm.environment.set("pfName", res)
var res2 = pm.variables.replaceIn("{{$randomLastName}}")
pm.environment.set("plName", res2)
var res3 = pm.variables.replaceIn("{{$randomInt}}")
pm.environment.set("ptPrice", res3)
```
#### Request Body:
```
{
    "firstname" : "{{pfName}}",
    "lastname" : "{{plName}}",
    "totalprice" : {{ptPrice}}

}
```
#### Response Body:
```
{
    "firstname": "Dr. Susana",
    "lastname": "Muller",
    "totalprice": 838,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2024-03-20",
        "checkout": "2024-03-22"
    },
    "additionalneeds": "Dinner"
}
```
### 7. Read After Partially Modify A Booking
#### URL: https://restful-booker.herokuapp.com/booking/3078
#### METHOD: GET
#### Response Body:
```
{
    "firstname": "Dr. Susana",
    "lastname": "Muller",
    "totalprice": 838,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2024-03-20",
        "checkout": "2024-03-22"
    },
    "additionalneeds": "Dinner"
}
```
### 8. Delete A Booking
#### URL: https://restful-booker.herokuapp.com/booking/3078
#### METHOD: DELETE
#### Response Body:
```
Created
```
### 9. Read After Delete A Booking
#### URL: https://restful-booker.herokuapp.com/booking/3078
#### METHOD: GET
#### Response Body:
```
Not Found
```
# Run Through Command-Prompt
  • Run Command for Console:
  ```
    newman run REST_API_Booking.postman_collection.json -e Env_REST_API_Booking.postman_environment.json
  ```
  • Run Command for Report:
  ```
    newman run REST_API_Booking.postman_collection.json -e Env_REST_API_Booking.postman_environment.json -r cli,htmlextra
  ```
# Newman Report Summary:
![image](https://github.com/Callick/Automated-Testing-of-REST-Booking-API-Using-POSTMAN-with-Newman-Report/assets/32848605/595ebf0f-9997-42c2-8708-0d2d52f0b131)
![image](https://github.com/Callick/Automated-Testing-of-REST-Booking-API-Using-POSTMAN-with-Newman-Report/assets/32848605/9ed54e78-25ae-48fe-a0a0-62b8cb133035)
![image](https://github.com/Callick/Automated-Testing-of-REST-Booking-API-Using-POSTMAN-with-Newman-Report/assets/32848605/5e4a100d-4b34-4163-aea0-bb44d8799928)
![image](https://github.com/Callick/Automated-Testing-of-REST-Booking-API-Using-POSTMAN-with-Newman-Report/assets/32848605/a507b176-540f-4fdb-a8da-9f71c8b9e6e3)



