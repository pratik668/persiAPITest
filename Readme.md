
# Accessibility Audit Tool APIs (JAVA)


## Version 1.0.0


**Table of contents**
- General Info
- Prerequisites
- Technologies
- User Guidelines - Setup for running using STS 
- User Guidelines - Setup for running using WAR file
- How to Use APIs
	- Crawler Controller API
	- Violation Controller API
	- TestAllURLExcel Controller API
	- HelpScrapper Controller API
- Features 
- Version History
- Contact
 -----------------------------------
 
**General info**
<br>
These are the API’s developed in Java, using technologies like Spring Boot, Selenium for Automation of testing and Axe-Core APIs for performing accessibility tests on webpages. It provides a simple and intuitive application programming interface to assist the user in testing and generating reports. These report helps the user to fix the violation of any desired website. The tool aids developers in identifying accessibility problems and features for WCAG 2.0, WCAG 2.1, Section 508 and AXE best standards. 

**Prerequisites**
   - Spring Tool Suite 4.x
   - Java Development Kit 8 or above 
   - Chrome driver (depends on the chrome browser version)
   - Stable internet connection


**Technologies**
   - JAVA 1.8.x
   - Spring Tool Suite 4.x
   - Awagger API documentation
-----------------------

## User Guidelines - Setup for running using STS 

**Importing Project:**
   - Unzip the code file.
   - To import the code zip file in STS - <br>
     File -->Import --> General --> Existing Projects into Workspace --> Next --> Select Root directory (browse the unzipped file) --> Search for nested projects --> Finish.

**Setup Config:**
<br>
After importing the project in STS, setup the project as follows-<br>
- Wait till all the dependencies are loaded in the project, stable internet connection is required. <br>
- Open “config.properties” file:<br>
- On left-side Package Explorer AccessibilityAuditToolApiApplication --> src/main/resources --> config.properties <br>
- In “config.properties” : 
  A chrome driver should be downloaded for the specific chrome browser version. If you are using Chrome version 88, please download Chrome Driver 88.0.4324.
  Official Website to download [chrome driver](https://chromedriver.chromium.org/downloads) <br>


  <b>1.	pathToChromeDriver -</b> copy paste the path location of the chrome driver that is installed on the machine.  
	e.g. pathToChromeDriver=C:\\chromedriver.exe <br>
  <b>2.	pathToStoreAllReport -</b> copy paste the path location of the folder where all the reports should be saved.  
	e.g. pathToStoreAllReport =C:\\Generated Reports\\Test <br>
	Here, Test is the folder name where all the reports will be saved. <br>
  <b>3.	pathToStoreReport -</b> copy paste the path location of the folder where any report should be saved.<br>
	e.g. pathToStoreReport =C:\\Generated Reports\\Test <br>
	Here, Test is the folder name where the specific report will be saved. <br>

<b>NOTE:</b>
Use Double Slashes ( \\ ) instead of Single Slash ( \ ) while setting paths and make sure the paths exist on the file system. These paths will be considered as default path while saving the reports, this can be changed at runtime as well.  <br>

---------------

## User Guidelines - Setup for running using WAR file:

1.	Make sure you have a tomcat server in your machine. If not [click here](https://tomcat.apache.org/download-80.cgi) to download .
2.	After downloading the tomcat server extract it any directory of your choice, then copy the WAR file of the API into the webapps folder.
 	<img src='.\API Screenshots\tomcat1.png'> <br>

3.	Then go to the bin folder and open terminal in that folder.
4.	After terminal is opened input the following command: “startup”.
	<img src='.\API Screenshots\tomcat2.png'> <br>

5.	After entering the command, the tomcat server will be up and running on your local machine. Now you are good to perform the API’s operations.
	<img src='.\API Screenshots\tomcat3.png'> <br>

------------

## HOW TO USE THE API’s:

### 1. Crawler Controller API:<br>
• <b>API Url:</b></br> " http://localhost:8050/AccessibilityAuditToolApi-0.0.1 SNAPSHOT/api/utility/crawling/geturls?url=http://127.0.0.1:5500/index.html " <br>
This API crawls the number of pages in the website and returns List of pages in the Website, the response is in the JSON format. It takes the base URL of the website as input parameter. 
Here base URL is: “http://127.0.0.1:5500/index.html”.<br>

Enter the API URL into the web browser or your choice of API Client like postman or swagger.
 <img src='.\API Screenshots\geturl.png'> 
After providing the input, the Crawler Controller API will return the crawled URLs from the given websites as shown below.
  <img src='.\API Screenshots\geturl1.png'> <br>

-----

### 2. Violation Controller API:
• <b>API Url (getvoilation):</b><br>" http://localhost:2280/api/utility/getvoilation?values=http://127.0.0.1:5500/index.html&values=cat.keyboard "<br>
This API gets the Accessibility violations for the URL, here it is "http://127.0.0.1:5500/index.html”, and this violation’s are in json format and "cat.keyboard" is the WCAG A11Y standards value we want to filter.

 Enter the API URL into the web browser or your choice of API Client like postman or swagger.
  <img src='.\API Screenshots\getviolation.png'><br>
After providing the API URL input, the Violation Controller API will return the violations of the given web page in the JSON format as shown below.
  <img src='.\API Screenshots\getviolation1.png'> <br>


<br>
<br>
<br>


• <b>API Url (downloadreport):</b><br> " http://localhost:2280/api/utility/downloadreport?values=http://127.0.0.1:5500/index.html@values=wcag2a "<br>
This API gets the Accessibility violations of the given web page and generates json and Excel file and return "urlname_timestamp.zip" as a response.

Enter the API URL into the web browser or your choice of API Client like postman or swagger.
  <img src='.\API Screenshots\downloadreport.png'> <br>

After providing the API URL input, the Violation Controller API will generate json and Excel file and return "urlname_timestamp.zip" as a response as shown below.
  <img src='.\API Screenshots\downloadreport1.png'> <br>




----

### 3. TestAllURLExcel Controller API:
•<b> API Url:</b> " http://localhost:2280/api/utility/getallreports " <br>
This API takes JSON object as input which contains the List of URLS for which accessibility violation report should be generated. API returns the response in "timestamp.zip", the zip file contains the Excel and Json file for each URL in json input.

Here we are using Postman as API client to perform post request. Here we have to provide the List of URL’s for which accessibility violation report should be generated in JSON format as API request body. After clicking on send the API will return the zip file consisting the required JSON and Excel files.
 
 <img src='.\API Screenshots\getallreports.png'> <br>





----

### 4. HelpScrapper Controller API:
•<b> API Url:</b><br>"http://localhost:2280/api/utility/gethelp?url=https://dequeuniversity.com/rules/axe/4.1/image-alt?application=axeAPI "<br>

This API takes the Help URL as input and return this help information to solve the violation. Here Help URL is: “https://dequeuniversity.com/rules/axe/4.1/image-alt?application=axeAPI” 

Enter the API URL into the web browser or your choice of API Client like postman or swagger.
  <img src='.\API Screenshots\helpscrapper.png'> <br>

After providing the API URL input, the HelpScrapper Controller API will return help information in JSON format as shown below.
 
 <img src='.\API Screenshots\helpscrapper1.png'> <br>

-----------

**Features**

- Able to crawl the site and generate the list of crawled URLs.
- Generate the audit report in xlsx and json format.
- Able to filter the json and xlsx reports by passing Tag names.
- While crawling first crawler checks whether the sites contains sitemap or not, if site don’t have the sitemap it will use its crawler.

----------

**Version History**
* 0.1
   * Initial Release


----------

**Contact**
<!--name and contact github pro Link-->
