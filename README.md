## TSTBox - Tableau Server Toolbox 0.1
The Tableau Server Toolbox provides a supported way to establish a Tableau DevOps workflow. It also provides a way to programmatically parse Tableau Workbook information into structure data which can support Tableau Data Linage. We're just getting started and have plans to expend what you find here. Please help us by submitting feedback, issues, and pull requests!

### Introduction
It's know that the amount of workbooks on our tableau server is more and more massive. It will be a mess if more than one person works on a workbook or fix an urgent bug. We download the workbook from Tableau Server, edit it and publish it again. Sometimes it can't even remeber what the last change is. To improve the situation, we need to introduce a version control mechanism to the workflow. But there are few ways to apply aversion control on Tableau on the internet. Hence, we try to build a tool by our own to sove this problem, here come the TSTBox.

### Features Include:
1. Sync workbooks from Tableau Server
2. Publish workbooks to Tableau Server programmaticall
3. Publish workbooks to Github

### How to Install it?
1. Install git and git lagre file system in your laptop
* You can download git large file system from this link: https://git-lfs.github.com/. The default install location is under the personl home directory.

2. Clone the whole respository to your local directory(anywhere under your home directory)
3. Install required python packages.
* The list of packages you need:
  * sqlparse
  * gitpython

4. The application uses the default path of Anaconda3. If you want to change it, please edit the path in the TSTbox.bat file.

### Config.yaml File
The Config.yaml which is in the root path of the project is a config file that contains the dashboard folder names on the server. If there is a new project created on the server, you need update this config file.

### The workflow of the TSTbox
1. Before editing any file, run 'git pull' in your directory.
2. Sync the workbook from tableau server.
3. Edit the workbook.
4. Pulish the workbook to Tableau Server Production.
5. Push the workbook to github

### The folder structure of Production path
Production 
|---------Folder1 
               |----------Dashboard1.twb 
               |----------Dashboard2(.twbx) 
                              |------Data 
                                       |--------Datasource 
                                       |--------Extracets 
                              |------Image 
                              |------Dashboard2.twb 
* When you are going to create new workbooks, please follow the structure, or you can publish workbooks to server first and download them to local then the structure will be created automatically.
* You can ignore the structure when you sync the workbook from Tableau Server because it's automatic sturctured.

### Serveral essential things you need to know
1. Please follow the workflow strictly
2. Never change the files' name under the Production folder.

Data lineage

What is Data Lieage and why we need it:
* Data Lineage is the way to describe what happens to data as it goes through diverse processes. It can help us trace how data has been collected and where values on the dashboard were deriving from.

We get three different objects from our data processes:
* Tableau workbooks
* Mysql views
* Mysql tables

Tables -> views -> Tableau workbooks

First, we need the relationship between values on dashboards and the colunms of presto view. Parsing the XML files can help us to get this information. As we can't parse table names directly from XML if there are some custom sqls applied, to establish some underlying guideline is an alternative way to meet this requirement. Second, we also need information about views in the databases. Which physical tables the views derive from is the essential information to establish a comprehensive data lineage. But we still can't find a good way to extract the info for now. The problem is how to parse tables name from SQL queries. One way is using some special characters to tag tables, and then we can trace the tags to get the tables name.
