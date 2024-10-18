# -Creation-of-a-data-Pipeline-

This project demonstrates the setup of two pipelines using Azure Data Factory to move and process data between Blob Storage and Azure Data Lake Storage, along with performing transformations on student and stock datasets.

---

## 1. Azure Data Factory Setup

### Setting Up Azure Data Factory & Creating Storage Accounts
To start, we set up **Azure Data Factory** and create the necessary storage accounts.

---

## 2. Create Blob Storage Account

### Blob Storage Setup
1. We created the first **Blob Storage Account** named `cpyblob`.
2. Inside the Blob Storage account, we created a container called `studentdatablob` where we uploaded a student dataset in `.csv` format.

### Azure Data Lake Storage Account Setup
We followed a similar process to create an **Azure Data Lake Storage Account**. While creating this account, we enabled **Hierarchical Namespaces** to support Data Lake Storage Gen2 features.

---

## Pipeline 1: Student Dataset

### Overview
In this pipeline, we process the student dataset by moving data from **Blob Storage** to **Azure Data Lake** and performing some data transformations.

### Steps:

#### Step 1: Creating Linked Services
1. Launch **Azure Data Factory**.
2. Navigate to **Manage** and create linked services for:
   - **Blob Storage** (`Blob Linked Service`)
   - **Azure Data Lake** (`Data Lake Linked Service`)
3. Ensure both connections are tested and linked correctly.

#### Step 2: Creating Datasets
1. Navigate to **Author → Datasets → Create New Datasets**.
2. Create datasets for both **Blob Storage** and **Azure Data Lake Storage**.
   - For the Azure Data Lake dataset, select **Delimited Text** as the file format.

#### Step 3: Creating Pipeline 1
1. Under **Author**, navigate to **Pipelines → Create New Pipeline**.
2. Define the source as **DelimitedTextBlob**.
3. Add a **Derived Column** transformation to calculate values for `Fedu` and `Medu`.

#### Step 4: Filtering and Transformations
1. Filter the dataset based on the following condition:

(Fedu > 3 && Medu > 2) && (Fedu + Medu > 5)

2. Order the data based on `Fedu + Medu`.

#### Step 5: Column Selection & Sinking
1. Select only the following columns: `School`, `Sex`, `Age`, `Medu`, `Fedu`, and `Fedu + Medu`.
2. Sink the transformed data into **DelimitedTextADL** (Azure Data Lake).

#### Step 6: Validation and Publishing
1. Click **Validate All** to check for errors.
2. If there are no errors, click **Publish**.
3. Check the destination dataset to confirm the data was transferred correctly.

### Output Data:
- The output data is stored in the **Destination Directory** in Azure Data Lake.

---

## Pipeline 2: AAL Stocks Dataset

### Objective
To analyze the market trend of **Apple (AAL)** stock data.

### Steps:

#### Step 1: Preparing the Dataset
1. Upload the AAL stock dataset (`.csv` file) to the **Blob Storage Account** created earlier.
2. Create a new container in the **Azure Data Lake Storage Account** named `aaladl`.

#### Step 2: Creating Datasets
1. In **Azure Data Factory Studio**, create new datasets for both **Blob Storage** and **Azure Data Lake Storage** using the linked services created previously.

#### Step 3: Creating Pipeline 2
1. Navigate to **Author → Pipelines → Create New Pipeline**.
2. In **Pipeline 2**, add a **Derived Column** transformation with the following:
- **True Range**: Expression `High - Low`
3. Add two more derived columns:
- **BUY SIGNAL**
- **SELL SIGNAL**

#### Step 4: Column Selection & Sinking
1. Select the relevant columns for further analysis.
2. Sink the output into the **Data Lake Storage** destination.

#### Step 5: Validation and Publishing
1. Validate the pipeline to ensure there are no errors.
2. Publish the pipeline.
3. Verify the output file in the destination folder.

### Output Data:
- The transformed stock data is stored in the **Destination Directory** of Azure Data Lake.

---

## Conclusion

In this project, we set up two pipelines using Azure Data Factory to process different datasets—one for student data and one for stock market analysis. The data was moved from Blob Storage to Azure Data Lake, and transformations such as filtering, derived column creation, and data sinking were performed to prepare the data for analysis.



