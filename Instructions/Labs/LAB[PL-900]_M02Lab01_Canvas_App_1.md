---
lab:
    title: 'Lab: Canvas App, Part 1'
    module: 'Module 2: Get Started with Power Apps'
---

# Module 2: Get Started with Power Apps
## Lab: Canvas App, Part 1

Scenario
========

Bellows College is an educational organization with multiple buildings on campus. Campus visits are currently recorded in paper journals. The information is not captured consistently, and there are no means to collect and analyze data about the visits across the entire campus. 

Campus administration would like to modernize their visitor registration system where access to the buildings is controlled by security personnel and all visits are required to be pre-registered and recorded by their hosts.

Throughout this course, you will build applications and perform automation to enable the Bellows College administration and security personnel to manage and control access to the buildings on campus.  

In part 1 this lab, you will design a Power Apps canvas app that college staff can use to manage visits for their guests.

High-level lab steps
======================

We will follow the below outline to design the canvas app:

-   Create the app from data using the phone form factor template
-   Configure a detail page with visit info
-   Configure an edit page to create to visits
-   Configure a gallery control to show the visits
-   Add filtering on the gallery data source to show only future visits

## Prerequisites

* Completion of Lab 1 - Data Modeling

Things to consider before you begin
-----------------------------------

-   What is the most prevalent form factor for the target audience?
-   Estimate the number of records in the system 
-   How to narrow the records selected to improve app performance and user adoption


Exercise \#1: Create Staff Canvas App
===============================

**Objective:** In this exercise, you will create a canvas app from a template and then modify it to include required data.

Task \#1: Create Canvas App
---------------------------

In this task, you will create a canvas app using the phone layout template based on Common Data Service. Using Visits as a selected entity from Common Data Service, the template will generate a Gallery - View - Edit app to manage campus visits.

1.  Open the Campus Management solution.

    -   Sign in to <https://make.powerapps.com>

    -   Select your **environment** at the top right, if it is not already set to your Bellows College environment.

    -   Select **Apps**.

2.  Create new canvas application

    -   Click **New app** and select **Canvas**.
    
    -   Select **Phone layout** under **Common Data Service**.
    
-   Select **Common Data Service** connection then click **Create**.

    -   Select **Visits** table
    
    -   Click **Connect**
    
    -   The **Welcome to Power Apps Studio** window may appear. Click **Skip**.
    
3.  Save application

    1.  Click **File > Save**.
    
    2.  Type the name of the app as **Campus Staff(DeploymentId)**
    
    3.  Press **Save**.

Task \#2: Configure Visits Detail Form
--------------------------------

In this task, you will configure the Detail form to view information about individual visit records.

1.  Select the Back arrow at the top left to go back to the app definition.
2. Expand **DetailScreen1** under **Tree view**
3.  Select **DetailForm1**
4.  Select **Edit fields** next to **Fields** in the right-hand panel.
5.  Click **Add field**
6.  Select the following fields:
    * Actual End
    * Actual Start
    * Building 
    * Code
    * Scheduled End
    * Scheduled Start
    * Visitor
7.  Click **Add**
8.  Rearrange fields in the **Fields** pane by dragging and dropping field names up or down. Recommended order is:
    * Code, Name, Building, Visitor, Scheduled Start, Scheduled End, Actual Start, Actual End
9.  To preserve work in progress, click **File** then click **Save**. Use the back arrow to return to the app.

## Task #3: Configure Visits Edit Form 

In this task, you will configure a form to edit information about individual visit records.

1.  Expand **EditScreen1** under **Tree view**
2.  Select **EditForm1**
3.  Select **Created On** field and press **Del** key to remove the field
4.  Select **Edit fields** in the properties panel
5.  Click **Add field**
6.  Select the following fields
    * Building 
    * Scheduled End
    * Scheduled Start
    * Visitor
7.  Click **Add**
8.  Rearrange fields in the **Fields** pane by dragging and dropping field names up or down. Recommended order is:
    * Name, Building, Visitor, Scheduled Start, Scheduled End
9.  To preserve work in progress, click **File** then click **Save**. Use the back arrow to return to the app.

Task \#4: Configure Visits gallery
---------------------------------------

In this task, you will configure the pre-generated gallery to display the title, start and end dates for the visit. 

1.  Expand **BrowseScreen1** under **Tree view**
2.  Select **BrowseGallery1**
3.  Select **TemplateSize** property from the property dropdown
4.  Replace the expression with the following `Min(150, BrowseGallery1.Height - 60)`. That will ensure sufficient space for additional information.
5.  Edit the gallery by pressing the pencil icon in the top left corner of the gallery (hover over the app preview and click the pencil icon).
6.  Select the Date Time field.
7.  In the formula bar at the top, change `ThisItem.'Created On'`to `ThisItem.'Scheduled Start'`
8.  Select the field again
9.  Press `CTRL-C` then `CTRL-V` to create a copy of the field.
10.  Using either mouse or keyboard, move the copied control down and align it with the other controls in the gallery, beneath the other Date Time field.
11.  In the formula bar at the top, change `ThisItem.'Scheduled Start'` to `ThisItem.'Scheduled End'`
12.  To preserve work in progress, click **File** then click **Save**. Use the back arrow to return to the app.

## Task #5: Add date filter

Because number of visits continuously grows, users need a feature to filter the visits gallery. For example, the user may want to see only the future visits. In this task, you will add ability to show visits only after a date selected by the user.

1. Select **Insert** menu at the top.

2. Click **Input** and select **Date picker**.

3. Using either keyboard or mouse, position the control below the search box.

4. Select **BrowseGallery1** 

5. Resize and move the gallery control so that it is located under the date picker and covers the screen. You can do this by clicking the resize icon at the top center of the gallery control and resizing the control to start after the date picker.

6. While still selecting **BrowseGallery1**, click the **Advanced** tab of the Properties pane and locate the **Items** property.

7. In the expression, locate `[@Visits]` and replace them with `Filter(Visits,'Scheduled End' >= DatePicker1.SelectedDate)`. Full expression should look like the following:

   ```
   SortByColumns(
   	Search(
        Filter(
        	Visits,
            'Scheduled End' >= DatePicker1.SelectedDate
           ),
           TextSearchBox1.Text,
       	"bc_code","bc_name"
       ),
     "bc_code",
     If(SortDescending1, Descending, Ascending)
   )
   ```
   
8. To preserve work in progress, click **File** then click **Save**. Use the back arrow to return to the app.

# Exercise #2: Complete the App

In this exercise you will test the application and, once successful, you will add it to your solution.

Task \#1: Test App
--------------------------

1.  Start the application

    -   Select the **BrowseScreen1** and press **F5**, or click the Play icon at the upper-right corner to preview the app.
    -   The application should load and show a list of visits. 
    -   Test the filter by selecting different dates in the date picker control
    -   Select a visit and verify that display form is working properly
    -   Return to the gallery and press + to create a new visit. Verify that edit form contains required fields including visitor, building, and scheduled start and end dates.
    -   Fill in the information and submit. Verify that the new record appears in the gallery.
    -   Press **ESC** key to close the app

2.  Save and publish the application

    -   Click **File** and then click **Save**.

    -   Click Publish.

    -   Click **Publish this Version**.

    -   Click the back arrow to navigate back to the app.

    -   Close the **Designer** browser window or tab.

    -   Click **Leave** if prompted when tried to close the browser window.


## Task #2: Add App to Solution and publish 

1. Open the Campus Management solution.
   * Sign in to <https://make.powerapps.com>
   * If the Environment displayed in the top right is not your Bellows College environment, select your **Environment**. 
   * Select **Solutions**.
   * Click to open the **Campus Management** solution.
2. Select **Add existing**, then click **App**, and then click **Canvas app**.
3. Select **Outside solutions** tab.
4. Select **Campus Staff** app, click **Add**.
5. Select **Publish all customizations**.

# Challenges

* Calendar view of all visits and filtering by date range
* Ability to create and manage contacts as part of the app
* How to display multiple meetings during a single visit

