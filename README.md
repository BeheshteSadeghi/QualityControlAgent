🤖***Automated Electronics QC Agent (n8n & Python)***

📖 **Overview**

The Automated Electronics QC Agent is a low-code automation solution designed to eliminate human error and latency from the Quality Control (QC) process in electronics manufacturing.

It ensures instant, rules-based validation of measured data against predefined design specifications and triggers immediate alerts via Telegram for critical failures.

This architecture leverages a Python-based data preprocessor for clean input and n8n as the powerful, visual workflow engine for validation, logging, and alerting.

✨ **Features**

Single-Line QC Focus: Dedicated validation and reporting for one specific production line/component.

Real-Time Validation: Instantly compares measured data (Measured_Value) against defined limits (Min/Max) to determine a PASS or FAIL status.

Instant Alerting: Triggers immediate, actionable notifications for FAIL results exclusively via Telegram.

Centralized Logging: Logs all test results into a Google Sheet for auditing and historical analysis.

Data Standardization: Uses a Python preprocessor to convert raw instrument CSV exports into a clean, standardized JSON format.

⚙️ **Technical Architecture & Flow**

The system operates in a three-stage pipeline:

Data Acquisition (Python): The Python script reads raw instrument data, standardizes it into a JSON payload, and sends it via HTTP POST to the n8n Webhook.

Validation Engine (n8n):

The Webhook Node receives the JSON payload.

The Function Node applies the specific Min/Max rules for the production line, appending a Test_Result (PASS/FAIL) to the data.

The IF Node splits the workflow based on the Test_Result.

***Reporting & Alerting:***

All results (PASS/FAIL): Are appended to the Google Sheets audit log.

FAIL results only: Are instantly sent down the parallel path to the Telegram node for urgent notification.


🚀 **Getting Started**

***Prerequisites***
You need the following accounts and software installed:

Python 3.x: Installed on the local machine connected to the testing instrument.

requests Library: For sending HTTP POST requests (pip install requests).

n8n Instance: A self-hosted or cloud instance of n8n.

Google Account: For Google Sheets credentials.

Telegram Bot: A configured Telegram Bot Token and Chat ID for alerts.

***Setup Steps***

Step 1: Define Standards & Data

Clone the Repository: Clone this repository to your local machine.

Review Standards: Ensure the qc_standards_v1.0.json file reflects the correct Min and Max tolerances for your components on Line A, B, and C.

Create Sample Data: Place your sample CSV files (instrument_output_line_A.csv, etc.) in the same directory as the Python script.

Step 2: Build the n8n Workflow

Create Webhook: In n8n, add a Webhook Node. Set the HTTP Method to POST.

Copy URL: Copy the generated Webhook URL and paste it into the N8N_WEBHOOK_URL variable in the Python script (unified_preprocessor.py).

Implement Logic: Add the Function Node (using the JavaScript code provided in the project documentation) and the subsequent Google Sheets, IF and Telegram nodes, configuring their respective credentials and expressions.

Step 3: Test and Activate

Activate Workflow: Turn the n8n workflow ON (not just in test mode).

Run Python: Execute the unified Python script to send test data.

Verify Outputs: Check your Google Sheet and Telegram for the logged and alerted results.

🤝 **Contribution**

Contributions are welcome! If you have suggestions for improving the logic, extending alert methods, or refining the preprocessor script, please submit a Pull Request.

📝 ***License***

This project is licensed under the MIT License - see the LICENSE file for details.
