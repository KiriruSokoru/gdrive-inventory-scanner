# Google Drive Security Inventory Scan

A Jupyter Notebook tool designed for **Security Auditing** and **Asset Management** of Google Drive environments. 

It scans all files accessible to the user (including Personal Drive and Shared Drives), inventories metadata, and identifies potential security risks such as publicly exposed files.

## 🚀 Features

*   **Complete Inventory:** Lists all files (`trashed = false`) with metadata (Name, MIME Type, Size, Dates).
*   **Access Audit:** Identifies the file owner and the running user's specific permissions (Owner/Writer/Reader).
*   **Public Exposure Detection:** Automatically flags files with "Anyone with the link" permissions (Public Read/Edit).
*   **Data Analysis:** Exports data to a Pandas DataFrame for easy filtering and reporting.

## 🛠 Prerequisites

*   A Google Account.
*   [Google Colab](https://colab.research.google.com/) (Recommended) or a local Jupyter environment.
*   No manual API setup required if running in Colab (uses default user auth).

## 📥 How to Run

1. Open the `.ipynb` file in Google Colab.
2. Run the cells sequentially.
3. **Authenticate:** When prompted, follow the link to authorize the notebook to access your Google Drive metadata.
   * *Note: The script requests `drive.metadata.readonly` scope.*
4. Wait for the progress bar (`tqdm`) to finish scanning.
5. Analyze the results in the `audit_df` DataFrame.

## 📊 Example Analysis

Once the scan is complete, you can run custom queries in new cells:

