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
* 1.	Defining Wing Attributes
* 2.	Defining Target table structure
* 3.	Defining Steps included in the import process
* 4.	Defining Measures associated with the Wing
* 5.	Defining Topic and Subtopic for Measures
* 6.	Defining Reports associated with the Wing
7.	Associate Report Columns with Measures
8.	Define Report filtering criteria

Figure 1 blow is the flow diagram representing the steps needed to create a new Wing in MONAHRQ using the open source framework. This once created, you will be able to import your XML file to create a new data Wing in MONAHRQ for the Host Users to use it for data import and reporting. A sample Wing XML file is defined in Appendix A.


<table class=MsoTableGrid border=1 cellspacing=0 cellpadding=0
 style='border-collapse:collapse;border:none'>
 <tr>
  <td width=623 colspan=4 valign=top style='width:467.5pt;border:solid windowtext 1.0pt;
  background:#D9D9D9;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'><b>Element Name: Target (</b><span
  style='color:#2E75B6'><a href="#Wing_Target_block" target="_blank"><b><span
  style='color:#2E75B6'>See XML</span></b></a></span><b>)</b></p>
  </td>
 </tr>
 <tr>
  <td width=145 valign=top style='width:108.6pt;border:solid windowtext 1.0pt;
  border-top:none;background:#BDD6EE;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'><b>Attribute</b></p>
  </td>
  <td width=68 valign=top style='width:51.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  background:#BDD6EE;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'><b>Value(s)</b></p>
  </td>
  <td width=120 valign=top style='width:90.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  background:#BDD6EE;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'><b>Required?</b></p>
  </td>
  <td width=290 valign=top style='width:217.8pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  background:#BDD6EE;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'><b>Description</b></p>
  </td>
 </tr>
 <tr>
  <td width=145 valign=top style='width:108.6pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Name</p>
  </td>
  <td width=68 valign=top style='width:51.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>String</p>
  </td>
  <td width=120 valign=top style='width:90.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Required</p>
  </td>
  <td width=290 valign=top style='width:217.8pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>The name of the wing target
  dataset, i.e. “New Wing”</p>
  </td>
 </tr>
 <tr>
  <td width=145 valign=top style='width:108.6pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>DbSchemaName</p>
  </td>
  <td width=68 valign=top style='width:51.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>String</p>
  </td>
  <td width=120 valign=top style='width:90.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Optional</p>
  </td>
  <td width=290 valign=top style='width:217.8pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>The name of the database table
  that will hold your data. The table name is typically prefaced with
  “Targets_” as part of the naming convention. For example, “Targets_NewWing”.
  If one is not provided by the developer, the system will prepend the
  “Targets_” prefix to the target dataset name following the conventions stated
  above.</p>
  </td>
 </tr>
 <tr>
  <td width=145 valign=top style='width:108.6pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Description</p>
  </td>
  <td width=68 valign=top style='width:51.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>String</p>
  </td>
  <td width=120 valign=top style='width:90.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Optional</p>
  </td>
  <td width=290 valign=top style='width:217.8pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>The description for the wing
  target dataset.</p>
  </td>
 </tr>
 <tr>
  <td width=145 valign=top style='width:108.6pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>IsReferenceTarget</p>
  </td>
  <td width=68 valign=top style='width:51.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Boolean</p>
  </td>
  <td width=120 valign=top style='width:90.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Optional</p>
  </td>
  <td width=290 valign=top style='width:217.8pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>A value of “true” means that
  the open source Wing is a supplementary wing and the data uploaded by the
  Host User using this Wing will be utilized in conjunction with other existing
  Wing target datasets for reporting purposes. A default value of false is used
  if the attribute is not <a>defined.</a><span class=MsoCommentReference><span
  style='font-size:8.0pt'><a class=msocomanchor id="_anchor_1"
  onmouseover="msoCommentShow('_anchor_1','_com_1')"
  onmouseout="msoCommentHide('_com_1')" href="#_msocom_1" language=JavaScript
  name="_msoanchor_1">[VK1]</a>&nbsp;</span></span></p>
  </td>
 </tr>
 <tr>
  <td width=145 valign=top style='width:108.6pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>AllowMultipleImports</p>
  </td>
  <td width=68 valign=top style='width:51.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Boolean</p>
  </td>
  <td width=120 valign=top style='width:90.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Optional</p>
  </td>
  <td width=290 valign=top style='width:217.8pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>A value of “true” means the end
  user will be allowed to upload multiple datasets into the target table. A
  value of “false” means only one dataset may be loaded into the target table
  at a time. When set to true, then previously uploaded dataset is automatically
  deleted if a new data file is imported by the Host User. Before the import
  begins. If an existing Wing dataset is already linked to a website, then user
  will be prompted to remove the reference to the linked website and delete
  manually before trying upload.  A default of true is used if the attribute is
  not <a>defined.</a><span class=MsoCommentReference><span style='font-size:
  8.0pt'><a class=msocomanchor id="_anchor_2"
  onmouseover="msoCommentShow('_anchor_2','_com_2')"
  onmouseout="msoCommentHide('_com_2')" href="#_msocom_2" language=JavaScript
  name="_msoanchor_2">[VK2]</a>&nbsp;</span></span></p>
  </td>
 </tr>
 <tr>
  <td width=145 valign=top style='width:108.6pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>DisplayOrder</p>
  </td>
  <td width=68 valign=top style='width:51.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Int</p>
  </td>
  <td width=120 valign=top style='width:90.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Optional</p>
  </td>
  <td width=290 valign=top style='width:217.8pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>If the attribute is not
  defined, a default value of 999 <a>is used. </a><span
  class=MsoCommentReference><span style='font-size:8.0pt'><a
  class=msocomanchor id="_anchor_3"
  onmouseover="msoCommentShow('_anchor_3','_com_3')"
  onmouseout="msoCommentHide('_com_3')" href="#_msocom_3" language=JavaScript
  name="_msoanchor_3">[VK3]</a>&nbsp;</span></span></p>
  </td>
 </tr>
 <tr>
  <td width=145 valign=top style='width:108.6pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Version</p>
  </td>
  <td width=68 valign=top style='width:51.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>String</p>
  </td>
  <td width=120 valign=top style='width:90.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Required</p>
  </td>
  <td width=290 valign=top style='width:217.8pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>The version of the wing in a
  major, minor and milestone format, i.e. “1.0.0”.</p>
  </td>
 </tr>
 <tr>
  <td width=145 valign=top style='width:108.6pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>IsDisabled</p>
  </td>
  <td width=68 valign=top style='width:51.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Boolean</p>
  </td>
  <td width=120 valign=top style='width:90.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Optional</p>
  </td>
  <td width=290 valign=top style='width:217.8pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>A value of “true” means the
  target wing is disabled and will not be displayed in the application. A
  default of false is used if the attribute is not defined.</p>
  </td>
 </tr>
 <tr>
  <td width=145 valign=top style='width:108.6pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Publisher</p>
  </td>
  <td width=68 valign=top style='width:51.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>String</p>
  </td>
  <td width=120 valign=top style='width:90.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Required</p>
  </td>
  <td width=290 valign=top style='width:217.8pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>The publisher of the wing, i.e.
  “MONAHRQ Developer”.</p>
  </td>
 </tr>
 <tr>
  <td width=145 valign=top style='width:108.6pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>PublisherEmail</p>
  </td>
  <td width=68 valign=top style='width:51.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>String</p>
  </td>
  <td width=120 valign=top style='width:90.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Required</p>
  </td>
  <td width=290 valign=top style='width:217.8pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>The email address of the
  publisher of the wing, i.e. <a
  href="mailto:support@monahrqdeveloperExample.com">support@monahrqdeveloperExample.com</a>.</p>
  </td>
 </tr>
 <tr>
  <td width=145 valign=top style='width:108.6pt;border:solid windowtext 1.0pt;
  border-top:none;padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>PublisherWebsite</p>
  </td>
  <td width=68 valign=top style='width:51.0pt;border-top:none;border-left:none;
  border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>String</p>
  </td>
  <td width=120 valign=top style='width:90.1pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>Optional</p>
  </td>
  <td width=290 valign=top style='width:217.8pt;border-top:none;border-left:
  none;border-bottom:solid windowtext 1.0pt;border-right:solid windowtext 1.0pt;
  padding:0in 5.4pt 0in 5.4pt'>
  <p class=MsoNormal style='line-height:normal'>The website address for the
  publisher, i.e. <a name="OLE_LINK4"></a><a name="OLE_LINK3"></a><a
  href="http://www.monahrqdeveloperExample.com">http://www.monahrqdeveloperExample.com</a>.</p>
  </td>
 </tr>
</table>
