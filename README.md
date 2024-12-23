# Tire Change Process / Customer-Related BPA with UiPath
# Overview

This project implements an automation for customer-related workflows of the tire change process using UiPath. The project utilizes UiPath automation capabilities and various dependencies for database, Gmail, Excel, Files/Folders handling and UI automation activities such as Screen Scraping and Browser Actions. 

## Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [Dependencies](#dependencies)
- [Contact](#contact)

##  Prerequisites
- UiPath Studio  

  Ensure that UiPath Studio is installed on your system. This project was developed using UiPath Studio Version 24.10.8.0. A compatible version is required for proper functionality.
- Windows Operating System

  The project targets the Windows framework, so a Windows environment is necessary.
- MongoDB

  A MongoDB database instance is required. Prepare a valid connection URI.
- Dependencies
  
  Dependencies will be resolved automatically when opening the project in UiPath Studio. Required libraries include:
  - Aspire.MongoDB.Driver
  - Microsoft.CodeAnalysis.VisualBasic
  - MongoDBMigrations
  - System.Security.Cryptography.ProtectedData
  - UiPath activities such as Database, Excel, UIAutomation, etc.
- Network Access
  Internet access is required for cloud-based MongoDB instances.
- UiPath Orchestrator (Optional)
- Required if you plan to deploy or schedule the automation.

## Installation
- Clone the repository:
git clone https://github.com/your-repo/BPA_Uebung3.git

- Restore the dependencies:
- Open the project in UiPath Studio.
- Ensure all dependencies are resolved automatically or restore them manually.

## Usage

Inputs

The workflow accepts the following input arguments:

- in_ConnectionUri: MongoDB connection string. 

  The customers database is stored in MongoDB.
- in_customerInformation: Customer information to process.

  Customer information is taken from the received e-mails.

Important variables

The workflow's most important variable is:

- rescheduleFlag: This variable analyzes the response of the customer per e-mail. (Initializion value: False)
    - If customer will respond to the Suggested Appointment with "Confirm" --> rescheduleFlag: False
    - If customer will respond to the Suggested Appointment with "Cancel" --> rescheduleFlag: False & Process Ends.
    - Otherwise, rescheduleFlag: True

Outputs

The workflow provides the following output arguments:

- out_Result: Result of the query related to existence of the current customer in DB.
  
Steps

Set up the input arguments in UiPath Orchestrator or during runtime.

Run the Main.xaml file to execute the workflow.

**How to Test** 
- After setting environment up, please consider that all required dependencies are downloaded. Otherwise, please download them from "Manage Packages".
- Run the Main.xaml file.
- The first "Wait for Email Received and Resume" activity waits for:
  - To receive an email which has at least one "Appointment" word either in Subject or Body.
- Then it sends an email to the customer titled "Request: Personal Information".
  - Please respond it with "Reply option and the email should be structured as below:
    
Name: XXX
    Surname: XXX
    Vehicle: XXX

- Then it checks for the existence of the user in DB, if not the user will be added within the workflow.
- Then it takes an appointment date & time, opening "https://fullcalendar.io/demos" website and click on the Appointment date, saves the appointment, takes the screenshot of the current page and stores under the project.
- Then it sends an information email regarding the appointment to the customer and waits until the customer will respond.
  - If customer will respond to the Suggested Appointment with "Confirm" --> rescheduleFlag: False
  - If customer will respond to the Suggested Appointment with "Cancel" --> rescheduleFlag: False & Process Ends.
  - Otherwise, rescheduleFlag: True
    - If reschedule is requested, the loop will continue to suggest another appointment date & time.
- Then it checks if the customer's service package covers the cost
  - If it covers, price = 0
  - If not, price is taken from a website for one wheel and manipulated for 4 wheels, and 2 Euros discount was applied.
- Then the invoice is generated and sends it within an email as attachment, stored under the project.
- Then the process ends.
  
## Features

🚀 **MongoDB Database Interaction** 
🚀 **Customer Information Processing**  
🚀 **Workflow-driven task automation**  
🚀 **Email handling, Excel processing, and UI automation**  

## Dependencies
The project uses the following dependencies:

- Aspire.MongoDB.Driver (9.0.0)
- Microsoft.CodeAnalysis.VisualBasic (4.12.0)
- Microsoft.Extensions.Configuration.Binder (9.0.0)
- MongoDBMigrations (2.2.0)
- System.Security.Cryptography.ProtectedData (9.0.0)
- UiPath.Database.Activities (1.9.0)
- UiPath.Excel.Activities (2.24.4)
- UiPath.FTP.Activities (2.4.0)
- UiPath.GSuite.Activities (2.8.22)
- UiPath.Mail.Activities (1.24.11)
- UiPath.MicrosoftOffice365.Activities (2.8.22)
- UiPath.System.Activities (24.10.7)
- UiPath.Testing.Activities (24.10.3)
- UiPath.UIAutomation.Activities (24.10.10)
- UiPath.Word.Activities (1.20.3)

Environment

Developed with UiPath Studio Version: 24.10.8.0

Target Framework: Windows


## Development

Main.xaml: The main workflow file that orchestrates the automation process.
project.json: Contains metadata and dependencies for the project.


## Contact

For further information or collaboration, please contact:

Berna Zehra Ural - bernazehraural@outlook.com 
