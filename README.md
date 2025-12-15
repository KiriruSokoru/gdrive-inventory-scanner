# Google Drive Inventory & Security Scanner

A Jupyter Notebook tool for **Security Auditing**, **Shadow IT Discovery**, and **Asset Management** within Google Drive.

This tool performs a deep scan of all files accessible to a user (including Shared Drives), creates a detailed inventory, and highlights security risks like public exposure or external ownership.

---

## 🚀 Key Features

*   **Complete Inventory:** Recursively lists all files (`trashed = false`) with metadata (Name, Size, MIME Type, Created/Modified Dates).
*   **Permission Audit:** Automatically determines the file owner and **your** specific role (e.g., `writer`, `commenter`, `reader`, or `owner`).
*   **Public Exposure Detection:** Flags files shared with "Anyone with the link" (Public Read/Edit).
*   **Shadow IT Discovery:** Helps identify files you don't own but have editing rights to (potential phishing/malware vectors).
*   **Data Export:** Generates a clean Pandas DataFrame (`audit_df`) ready for export to CSV/Excel.

## 🛠 Prerequisites

*   A Google Account.
*   [Google Colab](https://colab.research.google.com/) (Recommended) or a local Jupyter environment.
*   No complex API setup required if running in Colab (uses user-managed OAuth flow).

## 📥 Quick Start

1.  **Open the Notebook:** Upload `G_Drive_Inventory_Audit.ipynb` to Google Colab.
2.  **Run All Cells:** Execute the cells sequentially.
3.  **Authenticate:** When prompted, follow the Google authentication link to allow the notebook to read Drive metadata.
    *   *Note: The script requests `drive.metadata.readonly` scope.*
4.  **Wait for Scan:** A progress bar (`tqdm`) will show the scanning status.
5.  **Analyze:** The results are stored in the `audit_df` variable.

## 📊 Data Analysis Examples

After the scan is complete, copy and paste these snippets into a new code cell to find security issues:

### 1. Find "Public Write" Files (Critical Risk)
Find files that anyone on the internet can modify or delete.
```
critical_exposure = audit_df[ audit_df['public_level'] == 'Public Link (Edit) ⚠️' ]
print(f"Critical files found: {len(critical_exposure)}")
display(critical_exposure)
```

### 2. Find External Files I Can Edit (Shadow IT)
Find files owned by others (external accounts) that you have write access to.
```
external_edit = audit_df[ 
    (audit_df['doc_type'] == 'Google Sheet') & 
    (audit_df['my_role'] == 'writer') & 
    (audit_df['is_owner'] == False) 
]
display(external_edit.head())
```

### 3. Export Report to CSV
Save the full audit log to a file for Excel/Sheets.
```
audit_df.to_csv('drive_audit_report.csv', index=False)
print("Report saved to drive_audit_report.csv")
```

## 🔒 Security & Privacy

*   **Client-Side Execution:** This script runs entirely within your session.
*   **Metadata Only:** The script reads file names and permissions; it does **not** download file contents.
*   **No Data Exfiltration:** No data is sent to external servers or third-party APIs.

## License

MIT License.
