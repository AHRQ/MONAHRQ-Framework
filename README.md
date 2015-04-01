MONAHRQ-Framework
=================

The highly dynamic health care environment driven by the Affordable Care Act and other changes in federal law provides an opportunity for MONAHRQ to become a software tool that significantly expands transparency while driving innovation and collaborative development. The new architecture of MONAHRQ can be leveraged to accelerate the adoption of the software as a quality reporting solution for internal quality improvement and public reporting. 

With the redesign of MONAHRQ architecture in MONAHRQ 6.0, it is possible to add new data sources, reporting options, and website customization capabilities using the Open Framework. This enables the open source developer community to plug-in additional data sets and measures, and create new report types. This Framework adds extensibility to the MONAHRQ application.

As with most software, the expanded Framework functionality is a first step in enabling innovation and greater flexibility for Host Users. For this initial version, Host Users who have experience with software development or basic programming skills should be able to apply the information described below to add new datasets and create new report types for their MONAHRQ-generated website. At the same time, Host Users who are not familiar with programming and related technical issues are encouraged to team with an IT professional or developer who can assist them with using the Framework included with MONAHRQ 6.0. 

### What is MONAHRQ Open Source Framework?
The Framework allows you to add one or more new dataset types, define measures and report types, and customize report layouts in their MONAHRQ-generated websites. The Framework is divided into two main framework components, Wings and Flutters, explained below.

#### Wings
A “Wing” is defined as a modular interface for the MONAHRQ software that enables Host Users to import new data files into MONAHRQ. There are several types of Wings used by MONAHRQ. Each Wing can handle a discrete dataset type. Several Wings can be used throughout the process of preparing and publishing a MONAHRQ-generated website. In version 1.0 of the Framework, you can add datasets similar to the existing datasets, such as, Medicare Provider Charges, Inpatient Discharge, Emergency Department Treat-and-Release, and AHRQ Quality Indicators (QIs). This is done by defining the Wing in an XML file.   
Wings are comprised of an XML formatted manifest file, which contains the instructions and configuration details of the Wing. You will be able to import a Wing into the MONAHRQ software. Once the Wing is imported into MONAHRQ, the Host User can use it to import the new data files. 
Wings can be imported by using the “Import Wing” option in the MONAHRQ software settings section. During the import, the files will be copied to the appropriate directories and any required structural changes (database table creation) will be completed during this process.

#### Flutters

A “Flutter” lets you create new report layouts, style and flow. This process uses the components of the AngularJS framework, which is the same framework used in all MONAHRQ-generated websites. Developing a Flutter from scratch is largely an exercise in AngularJS development (https://angularjs.org/), an increasingly common process using the open source web framework developed by Google. Developers who create Flutters will be authoring the necessary controllers, services, views, and styling to build the reports. 

A set of module rules and configuration guidelines is available for Framework developers to use to ensure that a new report format, or Flutter, can be plugged into a MONHARQ generated website for use with a compatible dataset produced by a Wing. 

In a simple scenario, you will be able to use an existing generic “tabular report” format that is already part of MONAHRQ by copying the existing report template and transforming it into a new report, or Flutter. This is done by specifying within the Flutter’s configuration the report’s unique name, data file(s), how a data file’s fields map to table columns, and the table’s column model (e.g.: titles, data formatting, and sorting rules). In this scenario, the underlying JavaScript code doesn’t need to be customized. In a more complex scenario, the underlying JavaScript can be modified to achieve the developer’s desired results.

## Developers

The technical details on creating Wings and Flutters can be found in [Wiki](https://github.com/AHRQ/MONAHRQ-Framework/wiki) section of this repository.

