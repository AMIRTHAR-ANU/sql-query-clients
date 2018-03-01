# Generic Cloud Function for IBM Cloud SQL Query

This directory contains a simple IBM Cloud Function in Python that calls a custom SQL query in the IBM Cloud SQL Query service using the ibmcloudsql Python package. It prereqs the bx CLI tool and the cloud function plugin.

## Function parameters:
  * `api_key` - Your IAM API key for your IBM Cloud user or service ID with access to your SQL Query instance and COS bucket
  * `instance_crn` - The instance CRN of your SQL Query instance. Find it in IBM Cloud console dashboard for your instance. Press the `Instance CRN` button there to copy it toyour clipboard
  * `target_url` - Cloud Object Storage URL for the SQL result target. Format: `cos://<endpoint>/<bucket>/[<prefix>]`
  * `client_info` (optional) - Tracking information to identify your client application inside IBM cloud

## 1. Build using `build_cloud_function.sh`
This creates a virtual Python environmet with the required dependencies and packages everything up into `ibmcloudsql_cloudfunction.zip` and registers a Cloud Function called `ibmcloudsql_cloudfunction`into your IBM Cloud org and space.

## 2. Bind using `bind_cloud_function.sh` to your COS and SQL Query instances
This sets the required parameters for API key, instance CRN and COS URL for SQL results. You need to edit the script with your instance data before running it.

## 3. Call the function with a SQL statement using `call_cloud_function.sh`
This calls the function with a simple sample statement passing to the function as a function parameter. You can change the SQL statement text to any other statement that works for you and your data.

*Note*: you can also decide to provide or override the COS and SQL Query instance information at invocation time by passing the parameters there. You can also decide to register the function with a hard coded SQL statement text by providing the `sql` parameter in the bind script.

 * More background on [Python cloud function](https://console.bluemix.net/docs/openwhisk/openwhisk_actions.html#creating-python-actions) creation and handling.
 * [Python environments](https://console.bluemix.net/docs/openwhisk/openwhisk_reference.html#openwhisk_ref_python_environments) for cloud functions
 * IBM Cloud CLI [download](https://console.bluemix.net/docs/cli/reference/bluemix_cli/download_cli.html#download_install)
 * Cloud functions [CLI plug-in](https://console.bluemix.net/docs/openwhisk/bluemix_cli.html#cloudfunctions_cli)