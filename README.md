MONAHRQ-Framework
=================

The highly dynamic environment driven by the Affordable Care Act provides an opportunity for MONAHRQ to become a software tool that drives innovation and collaborative development. With its new software architecture, MONAHRQ can be leveraged to accelerate the adoption of quality reporting solutions for internal quality improvement and public reporting. 

### What is MOANHRQ Open Source Framework?
MONAHRQ Open Source Framework allows the Developers to add a new dataset type, define measures, report types, and customize the report layout in MONAHRQ generated website. The Open Source Framework is divided into two main components:

#### Wing Framework
A “Wing” framework is defined as a pluggable interface for MONAHRQ application that is capable of importing a data file to MONAHRQ. There are several types of Wings utilized by MONAHRQ. Each Wing can handle a discrete dataset type. Several Wings can be utilized throughout the process of preparing and publishing a website. In version 1.0 of Open Source Framework for Wing, the Developers can add a datasets like, Medicare Provider charge, Inpatient Discharge, Emergency Department Treat-and-Release, and AHRQ QI indicator output by defining it in an XML file.   
Wings are comprised of a XML formatted manifest. The Developers will be able to register a Wing (XML file) to the MONAHRQ application to automatically launch. Once plugged to MONAHRQ, Host User can use the Wing to import data files. 
Wings can be imported by utilizing the “Import Wing” option under the application settings section. During the import, the files will be copied to the appropriate directories and any required registration (database table creation, etc.) is completed during this process.

#### Flutters Framework

A “Flutter” framework lets the Developers author reports layout, style and flow by utilizing the components of the AngularJS framework upon which MONAHRQ generated website is developed. Developing a flutter from scratch is largely an exercise in AngularJS development. The developer would author the necessary controllers, services, views, and styling to build the reports. 

A set of module rules and configuration is available for the Open Source Framework Developers to ensure that a flutters can be plugged into a MONHARQ generated website for a compatible dataset. 
In a simple scenario, a Developer will be able to utilize an existing out-of-the-box generic “tabular report” Flutter by copying the existing Flutter and integrating it with a new report. This is done by specifying within the flutter’s configuration the report’s unique name, data file(s), how a data file’s fields map to table columns, and the table’s column model (for example: titles, data types, and sorting rules). The underlying JavaScript code doesn’t need to be customized in this scenario. In a more complex scenario, the underlying JavaScript can be modified to achieve the desired results.

The sections below explains the “Wings” and “Flutter” creation process in simple steps.

### Creating a New Wing
Your new wing will be defined by creating an XML file. This file will contain all of the information needed to define your Wing, the target table that will hold the data uploaded by the Host User, the import steps for uploading the data, measures and their definition that will be associated with the dataset, and the associated reports. We suggest you use an XML editor and associate the XML Schema (WingTemplateXmx.xsd) for intellisense when creating your wing. At a high level, your new wing will look like this:
<?xml version="1.0" encoding="utf-8" ?>
<Target>
  <Columns />
  <ImportSteps />
  <Measures />
  <Reports />
</Target>

#### Wing Creation Work Flow
A new wing creation process is an eight step process that starts with defining your Wing attributes and ends with defining the reports for the type of data that will be imported by the Host User using this Wing. These steps include:
1.	Defining Wing Attributes
2.	Defining Target table structure
3.	Defining Steps included in the import process
4.	Defining Measures associated with the Wing
5.	Defining Topic and Subtopic for Measures
6.	Defining Reports associated with the Wing
7.	Associate Report Columns with Measures
8.	Define Report filtering criteria

Figure 1 blow is the flow diagram representing the steps needed to create a new Wing in MONAHRQ using the open source framework. This once created, you will be able to import your XML file to create a new data Wing in MONAHRQ for the Host Users to use it for data import and reporting. A sample Wing XML file is defined in Appendix A.
