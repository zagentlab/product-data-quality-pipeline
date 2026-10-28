# Product Data Quality Pipeline

## Overview

This project is an n8n workflow that retrieves product data from an API, transforms the records into a consistent structure, validates product information, and routes records to different destinations.

The workflow demonstrates practical automation using API integration, data transformation, conditional validation, Google Sheets, and CSV export.

## Business Problem

Businesses that maintain product catalogs often receive product information from external APIs, suppliers, or different data sources.

Product records may contain invalid prices or other incomplete information. Manually reviewing every record can take time and increase the risk of errors.

## Solution

This workflow automates the initial product data processing and validation steps.

It retrieves product records, separates individual products, standardizes selected fields, and checks whether each product meets the configured validation rule.

Valid products are sent to Google Sheets and exported to a CSV file. Products that fail the validation rule are routed to a separate Google Sheets destination for review.

## Workflow

1. **Manual Trigger:** Starts the workflow.
2. **HTTP Request:** Retrieves product data from the DummyJSON Products API.
3. **Split Out:** Converts the products array into individual workflow items.
4. **Set:** Selects and renames product fields.
5. **IF:** Validates product data using a configured condition.
6. **Google Sheets:** Stores valid product records.
7. **Invalid Products:** Routes records that fail validation to a separate sheet.
8. **Spreadsheet File:** Generates a CSV file from valid records.

## Current Validation Rule

The current test validates product prices.

- Valid: price is greater than zero.
- Invalid: price is zero or negative.

The workflow can be extended with additional rules, such as checking missing product names, invalid stock quantities, and duplicate product IDs.

## Tools and Technologies

- n8n
- HTTP Request and JSON data
- DummyJSON Products API
- Google Sheets
- CSV export
- Conditional data validation

## Test Results

During testing, two products were assigned invalid prices.

The workflow routed:
- 8 products to the valid output.
- 2 products to the invalid output.

After restoring the original product data, the workflow was tested again.

## Setup

1. Import the workflow JSON file into an n8n instance.
2. Configure the required Google Sheets credentials.
3. Select the appropriate spreadsheets and sheets.
4. Execute the workflow and inspect both output paths.
5. Verify the generated CSV file.

Credentials and account-specific configuration must be supplied by the person deploying the workflow.

## Future Improvements

- Add validation for missing product names.
- Validate stock quantities.
- Detect duplicate product IDs.
- Record a reason for each invalid record.
- Prevent duplicate records when the workflow runs repeatedly.
- Add automated summaries and error notifications.

## Project Purpose

This project demonstrates how n8n can automate product data ingestion, transformation, validation, and export with minimal custom code.
