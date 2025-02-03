# Uploading Items into DynamoDB Using a JSON File

This repository provides a step-by-step guide on how to upload multiple items into an Amazon DynamoDB table using a JSON file. You'll learn how to prepare your JSON file, upload items using the AWS CLI, verify the upload, and even how to handle large datasets with a Python script.

## Prerequisites

- **AWS CLI:** Installed and configured with the proper credentials and region.
- **DynamoDB Table:** Ensure that you have created your DynamoDB table (e.g., `YourTableName`).
- **JSON File:** Create a JSON file (e.g., `data.json`) formatted for DynamoDB's batch write operation.

## Step 1: Prepare Your JSON File

Create a JSON file (e.g., `data.json`) with the following structure. Make sure to replace `YourTableName` and the attribute values as needed.

```json
{
  "YourTableName": [
    {
      "PutRequest": {
        "Item": {
          "PrimaryKey": { "S": "key1" },
          "Attribute1": { "S": "value1" },
          "Attribute2": { "N": "123" }
        }
      }
    },
    {
      "PutRequest": {
        "Item": {
          "PrimaryKey": { "S": "key2" },
          "Attribute1": { "S": "value2" },
          "Attribute2": { "N": "456" }
        }
      }
    }
    // You can add up to 25 items per batch.
  ]
}
```
Note:

- DynamoDB accepts a maximum of 25 items per batch write operation.
- Ensure that the data types match DynamoDB requirements (e.g., S for strings, N for numbers).
## Step 2: Upload Items Using AWS CLI
Use the following command to upload your items into the DynamoDB table:


```bash 
aws dynamodb batch-write-item --request-items file://data.json
```

This command tells the AWS CLI to use the JSON file data.json to perform a batch write operation on your DynamoDB table.

## Step 3: Verify the Upload
To confirm that the items have been successfully uploaded, run the following command:

```bash 
aws dynamodb scan --table-name YourTableName
 ```
This command will scan the table and display the items currently stored in it.

## Step 4: (Optional) Using a Python Script for Large Datasets
If you have more than 25 items or want to implement error handling (e.g., retrying unprocessed items), you can use the following Python script with Boto3:

```python
import json
import boto3

# Initialize the DynamoDB client
dynamodb = boto3.client('dynamodb')
table_name = 'YourTableName'

# Load the JSON file
with open('data.json') as f:
    data = json.load(f)

items = data[table_name]

# Process items in batches of 25
for i in range(0, len(items), 25):
    batch = items[i:i + 25]
    response = dynamodb.batch_write_item(RequestItems={table_name: batch})
    
    # Check for unprocessed items and handle them as needed
    unprocessed = response.get('UnprocessedItems', {})
    if unprocessed:
        print("Unprocessed items detected. Consider implementing a retry mechanism.")
```
### Note: This script reads the JSON file, processes the items in batches of 25, and checks for any unprocessed items that may need to be retried.

## Summary
- Prepare your JSON file with the correct structure and data types.
- Upload items using the AWS CLI command: `aws dynamodb batch-write-item --request-items file://data.json`
- Verify your upload by scanning the DynamoDB table.
- Use a Python script for handling large datasets or for advanced error handling.
Happy coding!
