---
title: Submit requests through Postman
permalink: /docapis_postman.html
categories:
- api-doc
keywords:
course: "Documenting REST APIs"
weight: 1.5
sidebar: docapis
section: likeadeveloper
---


## GUI clients make REST calls a little easier

When you're testing endpoints with different parameters, you can use one of the many GUI REST clients available. With a GUI REST client, you can:

*  Save your requests (and numerous variations) in a way that's easy to run again
*  More easily enter information in the right format
*  See the response in a prettified JSON view or a raw format
*  Include header information

## Common GUI clients

Some popular GUI clients include the following:

* [Postman](http://www.getpostman.com/)
* [Advanced REST Client](https://chrome.google.com/webstore/detail/advanced-rest-client/hgmloofddffdnphfgcellkdfbfbjeloo) (Chrome browser extension)
* [REST Console](https://chrome.google.com/webstore/detail/rest-console/cokgbflfommojglbmbpenpphppikmonn)
* [Paw](https://luckymarmot.com/paw) (Mac, $30)

Of the various GUI clients available, I think Postman is the best option, since it allows you to save both calls and responses, is free, works on both Mac and PC, and is easy to configure.

## Learn by doing, then deep dive into concepts

A lot of times abstract concepts don't make sense until you can contextualize them with some kind of action. In this course, I'm following more of an act-first-then-understand type of methodology. After you do an activity, we'll explore the concepts in more depth. So if it seems like I'm glossing over concepts things now, like what a GET method is or a resource URL, hang in there. When we deep dive into these points later, things will be a lot clearer.

## Make a request in Postman

1.  If you haven't already done so, download and install the [Postman app] at [www.getpostman.com](https://www.getpostman.com/). If you're on a Mac, choose the Mac app. If you're on Windows, choose the Chrome app. (Note that you must also have Chrome to run the Chrome app.)
2.  You'll make a REST call for the first endpoint (`aqi`) in the Mashape Weather API. Select **GET** for the method.
3.  Insert the endpoint into the main box (next to the method, which is GET by default): `https://simple-weather.p.mashape.com/aqi`
4.  Click the **Params** button (to the right of the box where you inserted the endpoint) and insert `lat` and `lng` parameters with specific values (other than `1`).

    {{site.data.alerts.note}} Only some countries are supported in the <code>aqi</code> call &mdash; specifically the United States, Singapore, Malaysia, Europe, and Australia. If the country isn't supported, you'll see "Not supported" in the API response. The AQI for Santa Clara, California is <code>lat: 37.3710062</code> and <code>lng: -122.0375935</code>. For Singapore, it's <code>lat: 1.3321256</code> and <code>lng: 103.7373503</code>. You can find latitude and longitude values from the URL in Google Maps when you go to a specific location.{{site.data.alerts.end}}

    <img src="images/googlemapslatlong.png" alt="Finding latitude and longitude on Google Maps" />

	When you add these `lat` and `lng` parameters, they will dynamically be added as a query string to the endpoint URI. The query string is the code followed by the `?` in the endpoint URL. A request URL only has one query string (one `?`). If you have additional parameters in the query string, they're joined with an ampersand `&` symbol.

5.  Click the **Headers** tab (below the GET button) and insert the key value pairs: `Accept: text/plain` and `X-Mashape-Key: APIKEY`. (Swap in your own API key in place of `APIKEY`.)

    Your inputs should look like this:

	<img src="images/postmannewinterface.png" alt="Postman request" />

7.  Click **Send**.

	The response appears, such as `52`. In this case, the response is text only. You can switch the format to HTML, JSON, XML, or other formats, but since this response is text only, you won't see any difference. Usually the responses are more detailed JSON, which allows you to select a specific part of the response to work with.

	{{note}}If you get a response that says "Unsupported," this means your `lat` and `lng` values aren't supported. Use the lat and lng values shown here (`?lat=33.8351523&lng=-117.986186`)." %}

## Save the request

1.  In Postman, click the **Save** button (next to Send).
2.  In the Save Request dialog box, create a new collection (for example, weather) by typing the collection name in the **"Or create new collection"** box.
3.  In the Request Name box at the top of the dialog box, type a friendly name for the request, such as "AQI endpoint".
4.  Click **Save.**

Saved endpoints appear in the left side pane under Collections.

## Make requests for the other endpoints

Enter details into Postman for the other two endpoints for the Mashape Weather API:

* weather
* weatherdata

{{important}}The Accept header tells the browser what format you will accept the response in. Whereas the first two endpoints (aqi and weather) are <code>text/plain</code>, the Accept header for the <code>weatherdata</code> endpoint is <code>application/json</code>." %}

When you save these other endpoints, click the arrow next to Save and choose **Save As**. Then choose your collection and request name. (Otherwise you'll overwrite the settings of the existing request.)

<img src="images/postmansaveas.png" alt="Save as" />

(Alternatively, click the **+** button on the new tab and create new tabs each time.)

## View the format of the weatherdata response in JSON

While the first two endpoint responses include text only, the weatherdata endpoint response is in JSON.

In Postman, make a request to the weatherdata API. Then toggle the options to **Pretty** and **JSON**.

<img src="images/postmanjsonresponse.png" alt="JSON response" />

The Pretty JSON view expands the JSON response into more readable code.

{% include tip.html content="To \"prettify\" code means to un-minify it and format it with white space that is readable." %}

For the sake of variety with GUI clients, here's the same call made in Paw:

<img src="images/pawexample.png" alt="Paw" />

Like Postman, Paw also allows you to easily see the request headers, response headers, URL parameters, and other data. However, Paw is specific to Mac only.

## Enter several requests for the Aeris API into Postman

Now let's switch APIs a bit and see some weather information from the Aeris API. Constructing the endpoints for the Aeris Weather API is a bit more complicated since there are many different queries, filters, and other parameters you can use to configure the endpoint.

Here are a few requests to configure for Aeris. You can just paste the requests directly into the URL request box in Postman and the parameters will auto-populate in the parameter fields.

Note that the Aeris API doesn't use a Header field to pass the API keys &mdash; the key and secret are passed directly in the request URL as part of the query string.

{% include note.html content="When you make the following requests, insert your own values for the <code>CLIENTID</code> and <code>CLIENTSECRET</code>." %}

Get the weather forecast for your area:

```
http://api.aerisapi.com/observations/Santa+Clara,CA?client_id=CLIENTID&client_secret=CLIENTSECRET&limit=1
```

In the response, find the wind speed and compare it with the wind from the Mashape API. Are they the same?

Get the weather from a city on the equator &mdash; Chimborazo, Ecuador:

```
http://api.aerisapi.com/observations/Chimborazo,Ecuador?client_id=CLIENTID&client_secret=CLIENTSECRET&limit=1
```

Find out if all the country music in Knoxville, Tennessee is giving people migraines:

```
http://api.aerisapi.com/indices/migraine/Knoxville,TN?client_id=CLIENTID&client_secret=CLIENTSECRET
http://api.aerisapi.com/indices/migraine/Knoxville,TN?client_id=CLIENTID&client_secret=CLIENTSECRET
```

You're thinking of moving to Arizona, but you want to find a place that's cool. Use the `normals` endpoint:

```
http://api.aerisapi.com/normals/flagstaff,az?client_id=CLIENTID&client_secret=CLIENTSECRET&limit=5&filter=hassnow
```

By looking at these two different weather APIs, you can see some differences in the way the information is called and returned. However, fundamentally both APIs have endpoints that you can configure with parameters. When you make requests with the endpoints, you get responses that contain information, often in JSON format. This is the core of how REST APIs work &mdash; requests and responses.
