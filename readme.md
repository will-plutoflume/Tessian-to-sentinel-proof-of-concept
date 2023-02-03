# Tessian <> Sentinel PoC

## ⚠️  The important part:
The Tessian platform provides an extensive set of APIs available in your portal under Integrations -> Tessian API.
While the APIs are supported by Tessian, all further integration into Sentinel, including the content of this repo is not officially supported by Tessian, and is provided simply as a proof-of-concept.

## What's in this repo
The setup used in this PoC uses an Azure Logic App to feed the Azure Log Analytics workspace behind a Sentinel instance with data from one or more Tessian instances.
The following files are provided:
- example_custom_log.json - This is used as the inital schema definition for a custom log format in Azure Log Analytics.
- tessian-logic-app.json - This is an example log app that gathers the API data, extends it a little to make things easier, and pushes it to sentinel.

## How to set all this up
### 1. Create custom log space for Tessian logs
- Visit your logs analytics workspace
- Navigate to Custom Logs (left hand pane) 
- Press 'Add custom log'
- Select the example_custom_log.json file included in this repo & press next
- Leave 'record delimiter' on 'New line' and press next
- Under collection path, select Linux and set the path value to '/tessian'
- Name the custom log 'TessianLogs'. The name will have _CL appended to it. (If you name it something else, you will need to find+replace TessianLogs_CL in the logic app defintion later). Press next.
- Press create

### 2. Create a logic app
- Navigate to 'Logic Apps' in Azure
- Press 'Add'
- Configure the resource group settings and name the logic app. Leave 'Plan type' on 'Consumption'. Press Next.
- Assign any tags you want. Press next.
- Review and create your logic app

### 3. Update logic app
- Navigate to the new logic app resource you created
- Select it. If prompted to select a template to start with, select 'blank logic app'
- On the left hand pane, switch to 'Logic app code view'
- Paste in the contents of 'tessian-logic-app.json' included in this repo
- Navigate to the bottom of the file
- Under 'parameters' in the JSON, you'll see a definition for 'azureloganalyticsdatacollector'
- There are two paths that contain information you need to replace. You will need:
- Your subscription ID
- The resource group name for your sentinel instance.
- The name of the region your sentinel instance is deployed in
- Replace the placeholder data in the 'connectionId' and 'id' defintions with the required information
