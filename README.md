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
