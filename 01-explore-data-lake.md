# Exercise 1 - Explore the data lake with Azure Synapse SQL On-demand and Azure Synapse Spark

## Overview

In this exercise, you will explore data using the engine of your choice (SQL or Spark).

Understanding data through data exploration is one of the core challenges faced today by data engineers and data scientists as well. Depending on the underlying structure of the data as well as the specific requirements of the exploration process, different data processing engines will offer varying degrees of performance, complexity, and flexibility.

In Azure Synapse Analytics, you can use either the SQL Serverless engine, the big-data Spark engine, or both.

The tasks you will perform in this exercise are:

- Explore the Data Lake with SQL On-demand and Spark
  - Task 1 - Explore the Data Lake with Synapse SQL On-demand
  - Task 2 - Explore the Data Lake with Synapse Spark

## Task 1 - Explore the data lake with Azure Synapse SQL On-demand

In this task, you will browse your data lake using SQL On-demand.

1. In a Microsoft Edge web browser, navigate to the Azure portal (`https://portal.azure.com`) and login with your credentials from the Lab Environment Details tab. Then select **Resource groups**.

   ![Open Azure resource group](./media/00-open-resource-groups.png "Azure resource groups")

2. Select the **Synapse Analytics** resource group.

   ![Open Synapse Analytics resource group](./media/00-open-synapse-resource-group.png "Resources list")

3. Select **SQLPool01** and **resume** it before starting the exercise.

   ![SQLPool01 is highlighted.](media/select-sql-pool.png "SQLPool01")

   ![Resume sqlpool](./media/00-resume-sqlpool.png "Resume")

4. Return to the resource group, then select the **Synapse Analytics** workspace.

   ![Open Azure Synapse Analytics workspace](./media/00-open-workspace.png "Azure Synapse workspace")

5. On the Synapse workspace blade, open Synapse Analytics Studio by navigating to the **Workspace web URL** from the overview page.

   > You can also Open synapse studio by clicking on **Open** under **Getting started->Open synapse studio**

   ![The Launch Synapse Studio button is highlighted on the Synapse workspace toolbar.](media/ex01-open-synapse-studio.png "Launch Synapse Studio")

6. In Synapse Analytics Studio, from the left panel click on the expand icon and navigate to the `Data` hub.

   ![Open Data hub in Synapse Analytics Studio](./media/data-hub-1.png)

   ![Open Data hub in Synapse Analytics Studio](./media/data-hub.png)

7. Switch to the `Linked` tab **(1)**. Under `Azure Data Lake Storage Gen2` **(2)**, expand the `asaworkspace<UniqueId>` primary data lake storage account **(3)**, and then select the `wwi` file system **(4)**.

   ![The ADLS Gen2 storage account is selected.](media/storage-factsale-parquet-1.png "ADLS Gen2 storage account")

8. Inside the selected file system, double-click to navigate to `factsale-parquet` -> `2012` -> `Q1` -> `InvoiceDateKey=2012-01-01` **(5)**.

9. Once you are in `InvoiceDateKey=2012-01-01` right-click the Parquet file and select `New SQL script - Select TOP 100 rows`.

   > A script is automatically generated. Run this script to see how SQL on-demand queries the file and returns the first 100 rows of that file with the header, allowing you to easily explore data in the file

   ![Start new SQL script from data lake file](./media/ex01-sql-on-demand-01.png "Create a new SQL script")

10. Ensure the newly created script is connected to the `Built-in` pool and select `Run`. Data is loaded by the built-in SQL pool and processed as if it was coming from any regular relational database.

    ![Run SQL script on data lake file](./media/ex01-sql-on-demand-02.png "Execute SQL script")

    > Note: SQL on-demand is now named as **Built-in**

11. Let us change the initial script to load multiple Parquet files at once.

    - In line 2, replace `TOP 100 *` with `COUNT(*)`.
    - In line 5, replace the path to the individual file with

    ```python
    https://<yourdatalake storage account name>.dfs.core.windows.net/wwi/factsale-parquet/2012/Q1/*/*
    ```

    > Note: Replace 'yourdatalakestorageaccountname' with the **Storage Account Name** provided in the environment details section on the right.

12. Select `Run` to re-run the script. You should see a result of `2991716`, which is the number of records contained in all the Parquet files within the `factsale-parquet/2012/Q1` directory.

    ![Run SQL on-demand script loading multiple Parquet data lake files](./media/ex01-sql-on-demand-03.png)

13. In Azure Synapse Analytics Studio, navigate to the `Develop` hub.

    ![Develop hub.](media/develop-hub.png "Develop hub")

14. Select the `Exercise 1 - Read with SQL on-demand` SQL script. Connect to **Built-in** and select **SQLOnDemand01** as the database. Select **Run** to execute the script.

    ![Run SQL on-demand script loading multiple CSV data lake files](./media/ex01-sql-on-demand-04.png)

    > This query demonstrates the same functionality, except this time, it loads CSV files instead of Parquet ones (notice the `factsale-csv` folder in the path). Parquet files are compressed and store data in columnar format for efficient querying, as compared to CSV files which are raw representations of data, but easily processed by a large number of systems. Oftentimes, you can encounter many file types stored in a data lake and must know how to access and explore those files. When you access CSV files, for instance, you need to specify the format, field terminator, and other properties to let the query engine understand how to parse the data. In this case, we specify a value of `2` for FIRSTROW. This indicates that the first row of the file must be skipped because it contains the column header, for instance.
    >
    > Here we use WITH to define the columns in the files. You must use WITH when using a bulk rowset (OPENROWSET) in the FROM clause. Also, defining the columns enables you to select and filter the values within.

## Task 2 - Explore the data lake with Azure Synapse Spark

1. Navigate to the `Data` hub, browse to the data lake storage account folder `wwi/factsale-parquet/2012/Q1/InvoiceDateKey=2012-01-01`, then right-click the Parquet file and select `New notebook->Load Data frame`

   ![Start new Spark notebook from data lake file](./media/ex01-spark-notebook-001.png "Create a new Spark notebook")

2. This will generate a notebook with PySpark code to load the data in a dataframe and display 10 rows with the header.

   ![New Spark notebook from data lake file](./media/ex01-spark-notebook-002.png "Review the notebook")
   
3. Disable the **Preview Features** option at the top right corner.
   
   ![Preview](./media/preview.png "Preview features")

4. Attach the notebook to a Spark pool.

   ![Run Spark notebook on data lake file](./media/ex01-attachsparkpool01.png "Attach notebook to Spark pool")

5. Select **Run all** on the notebook toolbar to execute the notebook.

   > **Note**: The first time you run a notebook in a Spark pool, Synapse creates a new session. This can take approximately 3 minutes.

6. As you can see, the output of the dataframe is displayed with 10 rows. To  display 100 rows with the header replace the last line of code with the following:

   ```python
   display(df.limit(100))
   ```

7. Rerun the notebook to see the result.

   ![Improve dataset formatting in Spark notebook](./media/ex01-spark-notebookrun-04.png "Execute notebook")

8. Notice the included charting capabilities that enable visual exploration of your data. Switch to **Chart** **(1)** view. Select **View Options** **(2)** and change the **Key** **(3)** to `CustomerKey` and **Values** **(4)** to `CityKey` and then click on Apply **(5)** button.

    ![View charts on data in Spark notebook](./media/ex01-spark-notebook-05.png "Review charted data")
    
9. Collapse the output as illustrated below.

    ![Collapse Output](./media/collapseoutput.png "Collapse Output")

10. Hover over the area just below the cell in the notebook, then select **{} Add code** to add a new cell. **{} Add code** won't be visible until you Hover the area in front of the arrow.

   ![The add code button is highlighted.](media/addcode.png "Add code")

11. Paste the following into the cell and **replace** `YOUR_DATALAKE_NAME` with the name of your **Storage Account Name** provided in the **environment details** tab on the right. You can also copy it from the first cell of the notebook above.

    ```python
    data_path = spark.read.load(
       'abfss://wwi@YOUR_DATALAKE_NAME.dfs.core.windows.net/factsale-csv/2012/Q1/*/*',
       format='csv',
       sep="|",
       header=True)

    display(data_path.limit(100))
    ```

12. Select the **Run cell** button to execute the new cell and then select the **Table** view in the output section.

    ![The new cell is displayed and the run cell button is highlighted.](media/notebook-new-csv-cell1.png "New cell to explore CSV files")

    > This notebook demonstrates the same functionality, except this time, it loads CSV files instead of Parquet ones (notice the `factsale-csv` folder in the path).

13. **Important**: Close the notebook by selecting the X in the top right of the tab and then select Close + discard changes. Closing the notebook will ensure you free up the allocated resources on the Spark Pool. Also, close the SQLscripts along with any open notebooks.

     ![The new cell is displayed and the run cell button is highlighted.](media/close-notebook.png "Close Notebook")
     
     ![The Close + discard changes button is highlighted.](media/notebook-close-discard-changes.png "Discard changes?")

## Summary

- In this module you have completed exploring the **Data Lake** with **Synapse SQL On-demand** and **Synapse Spark**. Now you can move on to the next module by clicking on the Next button at the bottom right of this page.
