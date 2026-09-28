# Import Data using Transform Maps (Spreadsheet)

## Project Description

This micro project focuses on importing structured data from an external spreadsheet into the ServiceNow platform using Import Sets and Transform Maps. The project simulates a real-world scenario where bulk employee data is received in Excel format and must be migrated into ServiceNow efficiently and accurately.

The spreadsheet data is first loaded into an Import Set table, which serves as a staging area, and a Transform Map is then configured to map source fields to the appropriate target table fields. Upon executing the transformation, records are created in the target table and validated to ensure data integrity.

This project helps beginners understand the end-to-end data import process in ServiceNow, including data loading, field mapping, transformation execution, and result verification.

## Step-by-Step Process

### Phase 1: Prepare the Sheets

1. Open New Google Spreadsheet.
2. Create a new Google Spreadsheet with sample data as shown in the project documentation.
3. Download the spreadsheet as `Sample Spreadsheet.xlsx` format.

### Phase 2: Create New Custom Table

**Navigation:** `Tables > Create New`

Create the following table:

- **Label:** Employee Test
- **Name:** `u_employee_test`

After creating and saving the Employee Test table:

1. Scroll down to the bottom of the table form.
2. Click **Show Form** to open the table form.
3. Locate the **Form Context Menu / Additional Actions** option on the left side of the form header.
4. Click the Form Context Menu / Additional Actions icon.
5. Click **Configure** and select **Form Layout**.
6. Click **New** to create a new field.
7. Create the following fields:

| Field | Type |
|---|---|
| Employee ID | String |
| Employee Name | String |
| Email | String |
| Department | String |
| Location | String |

8. Click **Save**.
9. Verify that the newly created fields are displayed on the Employee Test form.

### Phase 3: Import Set Table

**Navigation:** `Application Navigator → Load Data`

1. Click **Load Data** and create an import table.
2. Fill in the details:
   - **Label:** Employee Import
   - **Name:** `u_employee_import` (auto populated)
3. Click **Submit**.
4. After submitting, confirm the success message.
5. Click **Create Transform Map**.

### Phase 4: Create Transform Map

Create the Transform Map using the **Create Transform Map** button.

Use the following details:

- **Name:** Sample Spreadsheet Import
- **Source Table:** Employee Import
- **Target Table:** Employee Test

Then:

1. Click **Auto Map Matching fields**.
2. Click **Mapping Assist**.
3. Map the fields between the Source and Target tables.
4. Click **Save**.
5. Make sure both Source and Target table fields are mapped.
6. Click **Transform**.
7. Click the **Transform** button again when prompted.
8. Confirm that the success message appears.

### Phase 5: Transform Data & Validate

**Navigation:** Open the Employee Test Table from the Application Navigator.

After the import succeeds, all records are created in the Employee Test Table.

Use **Personalised List Columns** to rearrange the fields as required and click **OK**.

**Final Result:** All records are successfully imported into the ServiceNow system using Import Set and Transform Map.

### Phase 6: Enable Coalesce to Avoid Duplicate Records

In real projects, the same employee data may be imported multiple times. To prevent duplicate employee records, use **Coalesce**.

Steps:

1. Open the Transform Map under System LDAP / All menus.
2. Open the created Transform Map named **Sample Spreadsheet Import**.
3. Under the Related List, open the **Field Maps** section.
4. Make one field **Coalesce = True**.
5. Save the form.
6. Add data again in Excel format.

The Coalesce setting updates existing records when matching values are found instead of inserting duplicate records.

### Phase 7: Inserting New Data in Excel Format

Steps:

1. Navigate to **All menus**.
2. Search for **Load Data** under System Import Set.
3. Open **Load Data**.
4. Fill in:
   - **Import set table:** Existing table — `Employee Import`
   - **Source of Import:** Select File
   - **Sheet number:** `1`
   - **Header row:** `1`
5. Click **Submit**.
6. Run the Transform using the previously created Transform Map.
7. Click **Transform**.
8. Confirm the state is **Completed** and **Success**.
9. Open **Transform History** to check inserted, updated, and skipped values.
10. Open the Employee Test table to verify the inserted and updated records.

The project documentation describes a test where 4 rows are uploaded: 2 are inserted as new IDs and 2 existing IDs are updated with changed names and emails.

When the same sheet is uploaded again to the same Transform Map, the documentation records 4 ignored rows, with 0 inserted and 0 updated.

### Phase 8: Create Reports on Employee Test Table

**Navigation:** `All menus → Reports → Usage and Governance → Reports`

Create the following three reports.

#### Report 1: Employees by Department

- **Report name:** Employees by Department
- **Source Type:** Table
- **Table:** Employee Test
- **Type:** Pie chart
- **Group By:** Department
- **Aggregation:** Count

Run and save the report.

#### Report 2: Employees by Location

Configuration:

- **Report name:** Employees by Location
- **Table:** Employee Test
- **Type:** Bar Chart
- **Aggregation:** Count
- **Group By:** Location

Run and save the report.

#### Report 3: Employee List Report

Configuration:

- **Report name:** Employee List Report
- **Table:** Employee Test
- **Type:** List
- **Columns:**
  - Employee ID
  - Employee Name
  - Email
  - Department
  - Location

Run and save the report.

### Phase 9: Add Reports to Dashboard

#### Create Dashboard

**Navigation:** `All menus → Dashboards`

1. Open **All menus** and search for **Dashboards**.
2. Under **Self Service**, click **Dashboards**.
3. Click **Create Dashboards**.
4. Alternatively, the project documentation specifies the backend name `PA_DASHBOARDS.FORM`.
5. Click **New** to create a dashboard.
6. Dashboard name: **Employee Analytics Dashboards**
7. Save the form.

The documentation also describes using the `pa_dashboards` ACL and enabling **Admin Overrides** for the Create operation when access is required.

#### Add Reports to Dashboard

1. Open **Reports** under Usage and Governance.
2. Open **Employees by Department**.
3. Select **Edit Report**.
4. Click **Share**.
5. Select **Add to Dashboards**.
6. Choose **Employee Analytics Dashboards**.
7. Click **Add**.
8. Repeat the same process for:
   - Employees by Location
   - Employee List Report

The project documentation also notes that widgets can be added using the **+** icon and that users, groups, and roles can be restricted through the Share option.

## Project Outcome

The project implements an employee data management solution using ServiceNow Import Sets and Transform Maps.

Key outcomes described in the project documentation include:

- Employee data imported from spreadsheet format.
- Source fields mapped to target table fields.
- Transform Map used to process imported data.
- Coalesce used to avoid duplicate records.
- Existing employee records updated during repeated imports.
- New employee records inserted.
- Reports created for department, location, and employee lists.
- Reports consolidated into an Employee Analytics Dashboard.
- Import and employee data activity made visible through reports and dashboards.

## Conclusion

This project successfully implemented an automated employee data management solution using ServiceNow Import Sets and Transform Maps, ensuring accuracy, efficiency, and data integrity throughout the employee onboarding and update process.

A key enhancement was the use of Coalesce in the Transform Map. By enabling Coalesce on the Employee ID field, the system identifies existing employee records during imports and prevents duplicate records.

The project was also extended with Reports and Dashboards to provide meaningful insights and visibility into employee data and import activities. The reports cover:

- Total employee records
- Newly added employees
- Updated employee records
- Department-wise employee distribution
- Import success and error counts

These reports were consolidated into a Dashboard so administrators and HR teams can monitor employee data trends, import performance, and data quality from a centralized view.
