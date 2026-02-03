# HHD Data Import & Validation Using Import Sets

## Overview
This repository demonstrates how Holographic Handheld Device (HHD) records were imported into ServiceNow using Import Sets and Transform Maps. The focus is on loading external data, validating imported records, performing incremental updates, and preparing device information for operational use within the HHD application.

The implementation reflects a real-world scenario where device data collected outside of ServiceNow must be integrated accurately, updated over time, and validated to maintain data integrity.

## Use Case
As Infinity expands distribution of HHD devices, device registration data is collected through spreadsheets during pilot and rollout phases. This data must be imported into ServiceNow so devices can be tracked, assigned, and supported by internal teams.

In this scenario, Import Sets are used to stage HHD data, apply transformation logic, update existing records using coalescing, and populate the HHD configuration table. Validation steps ensure imported and updated records align with existing CMDB and user data before operational use.

This project simulates how a ServiceNow administrator manages both initial and incremental data imports for hardware tracking.

## Features
- Import Set creation for external HHD data
- Staging table generation and validation
- Transform Map configuration for record creation
- Incremental data updates using coalescing
- Verification of imported and updated HHD records

## Technologies Used
- ServiceNow Platform
- Import Sets
- Transform Maps
- CMDB
- Data Validation

## Implementation Walkthrough

### Objective
Import external HHD data into ServiceNow, perform incremental updates using Import Sets, and validate that records are created and maintained accurately within the HHD configuration table.

### Step 1: Prepare the Import Validation View
A dedicated list view was created to support validation of imported HHD records.

The view was configured to display key fields such as serial number, firmware version, asset tag, assigned user, and assigned user location. Dot-walking was used to surface related user information without duplicating fields on the HHD table.

This view established a consistent way to review imported data after transformation.

<img width="1873" height="508" alt="Screen Shot 2026-02-02 at 5 18 18 PM" src="https://github.com/user-attachments/assets/9077dbcd-28ca-402d-8ffc-e216031a224a" />

<img width="1890" height="214" alt="Screen Shot 2026-02-02 at 5 23 46 PM" src="https://github.com/user-attachments/assets/9153b54d-ea68-4039-87af-ce940b2e5fcc" />

### Step 2: Load External HHD Data
An Import Set was created using the Load Data process to stage external HHD records.

The spreadsheet containing HHD device information was uploaded, generating a new staging table. All records loaded successfully and remained in a pending state prior to transformation.

The staging table was reviewed to confirm record count and field alignment.

<img width="1890" height="386" alt="Screen Shot 2026-02-02 at 5 34 58 PM" src="https://github.com/user-attachments/assets/5092eb86-a04f-4e7e-aa3c-c778cd784397" />

<img width="1890" height="386" alt="Screen Shot 2026-02-02 at 6 05 20 PM" src="https://github.com/user-attachments/assets/a00e719b-c3cb-476e-b1b1-b28332b7c91e" />

<img width="1890" height="313" alt="Screen Shot 2026-02-02 at 6 07 17 PM" src="https://github.com/user-attachments/assets/a189c11f-f698-426f-8a32-3e03f49e8f9b" />

### Step 3: Configure the Transform Map
A Transform Map was created to map fields from the staging table to the Holographic Handheld HHD table.

Field mappings were configured to ensure device identifiers, firmware details, and assignment data were populated correctly during transformation. The map was set to create new records during the initial load.

<img width="1890" height="313" alt="Screen Shot 2026-02-02 at 6 10 44 PM" src="https://github.com/user-attachments/assets/66f48071-77e6-429f-bae7-523130245ee1" />

<img width="1890" height="313" alt="Screen Shot 2026-02-02 at 6 16 44 PM" src="https://github.com/user-attachments/assets/4e5d5460-b979-4922-8bb7-cabecccceaf5" />

<img width="1890" height="313" alt="Screen Shot 2026-02-02 at 6 18 22 PM" src="https://github.com/user-attachments/assets/6c720622-f036-4bea-86e9-a5ce8ba0ca77" />

### Step 4: Execute the Transformation
The Transform Map was executed to process the staged data.

New HHD records were created successfully in the target table, and transform history confirmed all records processed without errors.

<img width="1890" height="313" alt="Screen Shot 2026-02-02 at 6 19 26 PM" src="https://github.com/user-attachments/assets/38d7684c-9f23-4652-b3de-5c81c8f2c818" />

### Step 5: Validate Imported HHD Records
The HHD list view was reviewed to confirm:
- All expected records were created
- Firmware version and asset tag values populated correctly
- Assigned users and related location data displayed as expected

This validation confirmed that imported data aligned with operational requirements.

<img width="1890" height="313" alt="Screen Shot 2026-02-02 at 6 20 44 PM" src="https://github.com/user-attachments/assets/efe480bc-6e8f-4885-b3cf-e040620959ef" />

### Step 6: Prepare Incremental HHD Update Data
An updated spreadsheet containing changes to existing HHD records was uploaded using a new Import Set.

This dataset included modifications such as updated firmware versions and assignment changes for previously imported devices.

The staging table was reviewed to confirm updated values prior to transformation.

<img width="1890" height="347" alt="Screen Shot 2026-02-02 at 6 26 45 PM" src="https://github.com/user-attachments/assets/d3050bd4-cbb5-49b7-9b80-62154ef48d1d" />

<img width="1890" height="347" alt="Screen Shot 2026-02-02 at 6 37 57 PM" src="https://github.com/user-attachments/assets/35845e8c-9d2a-47f2-b834-06739569036d" />

### Step 7: Update the Transform Map for Incremental Loads
The existing Transform Map was updated to support incremental data updates.

The **Serial Number** field was configured as a coalesce field to ensure incoming records matched existing HHD records rather than creating duplicates.

This configuration enabled controlled updates to existing devices.

<img width="1890" height="288" alt="Screen Shot 2026-02-02 at 6 42 09 PM" src="https://github.com/user-attachments/assets/ece3846c-964d-4ae0-b20a-c7964858129d" />

<img width="1890" height="288" alt="Screen Shot 2026-02-02 at 6 50 35 PM" src="https://github.com/user-attachments/assets/dc9fa8e7-c234-4810-a071-af524f6d9cc9" />

### Step 8: Execute the Incremental Transformation
The Transform Map was executed against the updated Import Set.

Existing HHD records were successfully updated based on serial number matching, and transform history confirmed records were updated rather than inserted. Update was also confirmed by an added Updated column.


### Step 9: Validate Incremental Updates
The HHD list view was reviewed again to confirm:
- Firmware version updates were applied correctly
- Assignment changes reflected the updated spreadsheet
- No duplicate records were created

This validation confirmed that incremental updates were processed accurately.

<img width="1890" height="608" alt="Screen Shot 2026-02-02 at 7 10 37 PM" src="https://github.com/user-attachments/assets/d7e01b02-c3a3-46b7-af9f-505d4a8c8b92" />

## Lessons Learned
- Import Sets support both initial and incremental data loads
- Coalescing prevents duplicate records during updates
- Validation views simplify review of imported and updated data
- Transform Maps enable controlled and repeatable data changes
- Incremental imports are essential for maintaining long-term data accuracy
