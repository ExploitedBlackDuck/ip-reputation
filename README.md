# ip-reputation

## ipprep.py

This script uses the apivoid API to check the reputation of a list of IP addresses and writes the results to a CSV file. Here's a breakdown of what the script does:

Imports the necessary modules: requests, csv, and apivoid.

Sets up the apivoid API key.

Opens the file containing the list of IP addresses and reads them into a list.

Opens a new CSV file for writing and creates a CSV writer object.

Iterates through the list of IP addresses, sending a request to the apivoid API for each one.

If the request is successful, extracts the relevant information from the API response and prints it to the console.

Writes the extracted information to the CSV file.

Once all IP addresses have been processed, closes the CSV file and prints "Done!" to the console.

Note that you will need to replace "YOUR_API_KEY_HERE" with your actual apivoid API key in order for the script to work properly. Also, make sure to update the filename and path for the source file and CSV file as needed.

## apivoid.py

This is the Python module that provides a function for making a query to the APIVoid API. The module relies on the "requests" and "json" libraries, which need to be imported for it to work.

The "make_query" function takes two arguments: "endpoint" and "arguments". The "endpoint" argument specifies the API endpoint to query, while "arguments" is a dictionary that contains the API parameters needed for the query, such as the API key and the IP address to check.

The function sends a GET request to the specified endpoint with the given arguments and returns the response as a JSON object. If there's an error during the request, the function returns an empty string.

Additionally, the module includes a helper function called "get_detection_engines". This function takes a dictionary of detection engines and returns a string that lists the names of the engines that detected a particular threat.

Overall, this module provides a simple way to interact with the APIVoid API using Python.
