---
title: Make a cURL call
permalink: /docapis_make_curl_call.html
categories:
- api-doc
keywords:
course: "Documenting REST APIs"
weight: 1.7
sidebar: docapis
section: likeadeveloper
---

While Postman is convenient, it's hard to represent &mdash; in your documentation &mdash; just how to make the calls. Additionally, different users probably use different GUI clients, or none at all (preferring the command line instead).

Instead of describing how to make REST calls using a GUI client like Postman, the most conventional method for documenting request syntax is to explain how to make the calls using cURL.

cURL is a command-line utility that lets you execute HTTP requests with different parameters and methods. In other words, instead of going to web resources in a browser's address bar, you can use the command line to get these same resources, retrieved as text.

In this section, you'll use cURL to make the same requests you made previously with Postman.

## Prepare the weather request in cURL format

1.  Go back into the [Weather API on Mashape](https://www.mashape.com/fyhao/weather-13).
2.  Copy the cURL request example for the first endpoint (aqi) into your text editor:

    ```sh
	  curl --get --include 'https://simple-weather.p.mashape.com/aqi?lat=1.0&lng=1.0' \
      -H 'X-Mashape-Key: EF3g83pKnzmshgoksF83V6JB6QyTp1cGrrdjsnczTkkYgYrp8p' \
      -H 'Accept: text/plain'
    ```

3.  If you're on Windows, do the following:
    * Change the single quotation marks to double quotation marks
    * Remove the backslashes (`\`)
    * Add `-k` after `--get`  as well to work around security certificate issues.

    The request should now look like this:

    ```sh
    curl --get -k --include "https://simple-weather.p.mashape.com/aqi?lat=1.0&lng=1.0" -H "X-Mashape-Key: APIKEY" -H "Accept: text/plain"
    ```

4.  Swap in your own API key in place of `APIKEY`.

    {: .note}
In the instruction in this course, <code>APIKEY</code> will always be used instead of an actual API key. You should replace that part with your own API key.

## Make the request in cURL (Mac)

1.  Open a terminal. To open Terminal, press **Cmd + space bar** and type **Terminal**.

	  {: .tip}
Instead of using Terminal, download and use [iTerm](https://www.iterm2.com/) instead. It will give you the ability to open multiple tabs, save profiles, and more.

2.  Paste the request you have in your text editor into the command line.

    My request for the Mashape Weather API looks like this:

    ```sh
	  curl --get --include 'https://simple-weather.p.mashape.com/aqi?lat=1.3319164&lng=103.7231246' -H 'X-Mashape-Key: APIKEY' -H 'Accept: text/plain'
    ```

    For the Aeris Weather observations endpoint, it looks like this:

    ```sh
	  curl --get --include "http://api.aerisapi.com/observations/santa%20clara,ca?client_id=CLIENTID&client_secret=CLIENTSECRET" "Accept: application/json"
    ```

3.  Press your **Enter** key.

    You should see something like this as a response:

    <img src="images/aqi_curl_response.png" alt="cURL call" />

    The response is just a single number: the air quality index for the location specified. (This response is just text, but most of the time responses from REST APIs are in JSON.)

## Make the request in cURL (Windows 7)

1.  Copy the cURL call from your text editor.
2.  Go to **Start** and type **cmd** to open up the commandline. (If you're on Windows 8, see [these instructions for accessing the commandline](http://pcsupport.about.com/od/windows-8/a/command-prompt-windows-8.htm).)
3.  Right-click and then select **Paste** to insert the call. My call for the Mashape API looks like this:

    ```sh
	  curl --get -k --include "https://simple-weather.p.mashape.com/aqi?lat=1.3319164&lng=103.7231246" -H "X-Mashape-Key: APIKEY" -H "Accept: text/plain"
    ```

    For the Aeris endpoint, it looks like this:

    ```sh
    curl --get --include "http://api.aerisapi.com/observations/santa%20clara,ca?client_id=CLIENTID&client_secret=CLIENTSECRET" -H "Accept: application/json"
    ```

    The response from Mashape looks like this:

    <img src="images/commandline.png" alt="Command line Windows" />


## Single and Double Quotes with Windows cURL requests

Note that if you're using Windows to submit a lot of cURL requests, you'll eventually run into issues with the single versus double quotes. Some API endpoints (usually for POST methods) require you to submit content in the body of the message request. The body content is formatted in JSON. Since you can't use double quotes inside of other double quotes, you run into issues in submitting cURL requests.

Here's the workaround. If you have to submit body content in JSON, you can store the content in a JSON file. Then you reference the file with an `@` symbol, like this:

```sh
curl -H "Content-Type: application/json" -H "Authorization: 123" -X POST -d @mypostbody.json http://endpointurl.com/example
```

Here cURL will look in the existing directory for the mypostbody.json file, but you can also reference the complete path to the JSON file.

## Make cURL requests for each of the weather endpoints

Make a cURL request for each of the weather endpoints for both the Mashape weather endpoints and the Aeris Weather endpoints, similar to how you made the requests in Postman.
