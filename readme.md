# Tessian <> Sentinel PoC

## The important part:
The Tessian platform provides an extensive set of APIs available in your portal under Integrations -> Tessian API.
While the APIs are supported by Tessian, all further integration into Sentinel, including the content of this repo is not officially supported by Tessian, and is provided simply as a proof-of-concept.

## What's in this repo
The setup used in this PoC uses an Azure Logic App to feed the Azure Log Analytics workspace behind a Sentinel instance with data from one or more Tessian instances.
The following files are provided:
- example_custom_log.json - This is used as the inital schema definition for a custom log format in Azure Log Analytics
- tessian-logic-app.json - This is an example log app that gathers the API data, extends it a little to make things easier, and pushes it to sentinel
