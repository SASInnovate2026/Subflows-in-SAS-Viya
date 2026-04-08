# Subflows in SAS Viya

## Exercise Description
In this hands-on workshop, you will create a flow to import and clean a table containing car data. Then, you'll use the flow as a subflow in an existing flow that joins and analyzes car data.

## Workshop Preparation

1. Confirm that the virtual lab opens on the **SAS Studio** *Start Page* in a Google Chrome window.

   ![SAS Studio start](images/SASStudioStart.png)

1. Open a new tab in the *Google Chrome* browser.
1. Select **Learning Labs &#10132; Subflows-in-SAS-Viya** to open the GitHub repository for the workshop.

   ![GitHub bookmarks](images/Bookmarks.png)

   ![GitHub landing page](images/GitHubLanding.png)

1. Select the **data** folder, then open **Car_Make_Info.csv**. Select ![Download](images/Download.png) to download the CSV file.

   ![Download CSV file](images/DownloadCSV.png)

1. Return to the main repository folder.
1. Select the **flows** folder, then open **Join Car Data.flw**. Select ![Download](images/Download.png) to download the flow file.

   ![Download Flow file](images/DownloadFlow.png)

1. Return to the *SAS Studio* tab.
1. Select ![SAS Content icon](images/SASContentIcon.png) to view the **SAS Content** pane.
1. Right-click **My Folder** and select **Upload files**.

   ![My Folder](images/MyFolder.png)

1. Select **+ Add files** in the *Upload Files* window.
1. In the File Explorer, navigate to the **Downloads** folder. Hold down the *Shift* key, then select **Join Car Data.flw** and **Car_Make_Info.csv**. Click **Open** to add the files to SAS Studio.

   ![Select files](images/SelectFiles.png)

1. Keep the default selections for the file encoding, then click **Upload** to confirm the upload of all files to *My Folder*.

   ![Upload files](images/UploadFiles.png)

1. If necessary, select **My Folder** and click ![Refresh icon](images/RefreshIcon.png) to refresh the file list.

   ![Refresh files](images/RefreshFiles.png)

## Create Flow *Import CAR_MAKE_INFO.flw*

1. Select **New &#10132; Flow** to create a new flow.
1. Click and drag **Car_Make_Info.csv** onto the flow canvas. The file will automatically appear in an *Import File* node.

   ![Add CSV data](images/AddCSVData.png)

1. On the *Options* tab, click ![Analyze](images/Analyze.png) to analyze the file contents.
1. Select *Preview and Modify Data* to view the file information. The imported file should have **3** columns and **37** rows.

   ![Preview and Modify Data](images/PreviewAndModifyData.png)

   > &#9998; Note that each **WEBSITE** URL starts with `https://` and that **PARENT COMPANY** values vary in casing.

1. Right-click the output port of the *Import File* node and select **Add a table** to add an output table to the node.
1. On the *Table Properties* tab, type the following:
   * Library: **WORK**
   * Table name: **CAR_MAKE**

   ![Add CAR_MAKE](images/AddCAR_MAKE.png)

1. Select ![Rearrange nodes](images/RearrangeNodes.png) to rearrange the nodes in the flow.

   > &#9998; You may have to collapse the **SAS Content** pane to view the *Arrange Nodes* option on the flow toolbar.

1. Select ![Save](images/Save.png) to save the flow.
1. In the *Save As* window, Navigate to **SAS Content &#10132; My Folder**.
1. Enter **Import CAR_MAKE_INFO** for the file name and click **Save**.

   ![Saved flow](images/SavedFlow.png)

1. Select ![Run](images/Run.png) to run the flow. Review the **Submitted Code and Results** and confirm that **CAR_MAKE** was created with **3** columns and **37** rows.

   ![CAR_MAKE results](images/CAR_MAKEResults.png)

1. Select ![Steps](images/Steps.png) to view the **Steps** pane.
1. Expand *Data Quality*, then click and drag the **Clean Data** step onto the flow canvas. Draw an arrow to connect **CAR_MAKE** to the input port of **Clean Data**.

   > &#9998; To connect two nodes in a flow, click from the right edge (for data) or output port (for steps) of the first node, then drag to the left edge (for data) or input port (for steps) of the second node.

   ![Add Clean Data](images/AddCleanData.png)

1. Keep the default QKB locale selection, **English (United States)**, on the *QKB Locale* tab.

   ![QKB Locale](images/QKBLocale.png)

1. Select the *Standardization* tab, then check the box to **Enable standardization**. This will surface additional step options.
1. Configure standardization as follows:
   * Select column: **WEBSITE**
   * Definition: **Website**
   * Column options: **Replace existing column**

   ![Configure standardization](images/ConfigureStandardization.png)

1. Select the *Casing* tab, then check the box to **Enable casing**. This will surface additional step options.
1. Configure casing as follows:
   * Select column: **PARENT COMPANY**
   * Definition: **Proper (Organization)**
   * Column options: **Replace existing column**

   ![Configure casing](images/ConfigureCasing.png)

1. Right-click the output port of the *Clean Data* node and select **Add a table** to add an output table to the node.
1. On the *Table Properties* tab, type the following:
   * Library: **WORK**
   * Table name: **CAR_MAKE_CLEAN**

   ![Add CAR_MAKE_CLEAN](images/AddCAR_MAKE_CLEAN.png)

1. Select ![Rearrange nodes](images/RearrangeNodes.png) to rearrange the nodes in the flow.
1. Select ![Save](images/Save.png) to save the flow.
1. Select ![Run](images/Run.png) to run the flow. Review the **Submitted Code and Results &#10132; Output Data** and confirm that **CAR_MAKE_CLEAN** was created with **3** columns and **37** rows.

   ![CAR_MAKE_CLEAN Results](images/CAR_MAKE_CLEANResults.png)

   > &#9998; Note that each **WEBSITE** URL now starts with `www.` and that **PARENT COMPANY** values are now cased consistently.
1. When finished reviewing the results, close **Import CAR_MAKE_INFO.flw**.

## Add a Subflow to an Existing Flow

1. In SAS Studio, select **Options &#10132; Reset SAS Session**.

   ![Reset SAS Session](images/ResetSASSession.png)

1. Select ![Libraries icon](images/LibrariesIcon.png) to view the **Library Connections** pane. Select the **WORK** library and confirm that it has no contents.

   ![Check WORK Library](images/CheckWorkLibrary.png)

1. Select ![SAS Content icon](images/SASContentIcon.png) to view the **SAS Content** pane.
1. Navigate to **My Folder** and double click **Join Car Data.flw** to open the flow.

   ![Join Car Data Flow](images/Join%20Car%20Data%20Flow.png)

   > &#9998; This flow joins the **SASHELP.CARS** and **WORK.CAR_MAKE_CLEAN** tables, then extrapolates the joined data to create reports and charts.

1. Select ![Run](images/Run.png) to run the flow. Review the **Submitted Code and Results** and confirm that the flow fails because **WORK.CAR_MAKE_CLEAN** does not exist.

   ![Error messages](images/ErrorMessages.png)

1. Select the **Flow** tab to return to the flow canvas.
1. Select ![Submission Order button](images/SubmissionOrder.png) (on the right side of the flow canvas) to open the *Submission Order* properties pane.
1. The existing swimlane, *Join Car Data*, appears. Select ![Add swimlane](images/AddSwimlane.png) to add a second swimlane to the flow.
1. Enter **Import CAR_MAKE_INFO** for the name of the new swimlane (replacing the default name, *Swimlane 2*.)
1. With the *Import CAR_MAKE_INFO* swimlane selected, select ![Move to Top](images/MoveToTop.png) to move that swimlane to the top position.

     ![Add new swimlane](images/AddNewSwimlane.png)

1. Select ![SAS Content icon](images/SASContentIcon.png) to view the **SAS Content** pane.
1. Navigate to **My Folder**. Click and drag **Import CAR_MAKE_INFO.flw** onto the flow canvas *and* in the *Import CAR_MAKE_INFO* swimlane.

   ![Add Subflow](images/AddSubflow.png)

1. Select ![Save](images/Save.png) to save the flow.
1. Select ![Run](images/Run.png) to run the flow. The flow now runs successfully.
1. Review the results of each portion of the flow by reviewing the *Output Data* and *Results* on the **Submitted Code and Results** tab.

   * The **Query** step creates the output table **CARS_INFO**, which contains 17 columns and 394 rows.

     ![CARS_INFO Results](images/CARS_INFOResults.png)

   * The **Characterize Data** step prints a report and a chart on the frequencies of the **PARENT COMPANY** values in **CARS_INFO**. The most frequent value is *General Motors*, followed by *Ford Motor Company*, *Toyota Motor Corporation*, and *Volkswagen Group*.

     ![Characterize Data results](images/CharacterizeDataResults.png)

   * The **Branch Rows** node subsets **CARS_INFO** based on *PARENT COMPANY* values and creates three output tables: **FORD_MOTOR_COMPANY**, **GENERAL_MOTORS**, and **TOYOTA MOTOR CORPORATION**.

     ![Branch Rows results](images/BranchRowsResults.png)

   * The **Pie Chart** nodes create pie charts showing the frequency of vehicle types in each of the subsetted tables.

     ![Pie chart results 1](images/PieChartResults1.png)

     ![Pie chart results 2](images/PieChartResults2.png)

     ![Pie chart results 3](images/PieChartResults3.png)

## Exercise Completed

You have completed the exercise for **Subflows in SAS Viya**.

**THANK YOU FOR ATTENDING THIS SESSION!**

**PLEASE COMPLETE THE WORKSHOP EVALUATION!**
