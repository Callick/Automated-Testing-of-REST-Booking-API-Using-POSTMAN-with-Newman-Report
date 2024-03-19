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
  •	Open Postman </br>
  •	Click on the Import button</br>
  • Select the file from the repository</br>
**2. Import the Postman environment:** </br>
  •	In Postman, click on the gear icon in the top right corner.</br>
  •	Select Import and choose the file.</br>
**3. Newman and Report Installation Process:** <br/>
  •	Newman Install Command</br>
   npm install -g newman <br/>
  •	Newman Html Report Install Command:<br/>
   npm install -g newman-reporter-htmlextra
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
