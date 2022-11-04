---
title: Signal timed metadata with Azure Media Services
description: Timed metadata is custom data that is inserted into a live stream. Both the data and its insertion timestamp are preserved in the media stream itself. This is so that clients playing the video stream can get the same custom metadata at the exact same time in relation to the video stream. With timed metadata you can add interactivity elements to the live stream such as a poll, add information related to the video content such as speakers, product links, sports player stats, etc. and add metadata about the video such as GPS location, time, etc.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 11/04/2022
ms.author: inhenkel
---

# How to signal timed metadata with Azure Media Services

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Timed metadata is custom data that is inserted into a live stream. Both the data and its insertion timestamp are preserved in the media stream itself. This is so that clients playing the video stream can get the same custom metadata at the exact same time in relation to the video stream. With timed metadata you can:

- Add interactivity elements to the live stream such as a poll.
- Add information related to the video content such as speakers, product links, sports player stats, etc.
- Add metadata about the video such as GPS location, time, etc.

## Delivery, post URL and request

Azure Media Services delivers the timed metadata as part of the video stream. Timed metadata is sent to a live event via a POST to the endpoint for timed metadata.

### POST URL

The format of the timed metadata endpoint is based on the RTMP ingest URL for the live event. For example:

`https://<<LIVEEVENTNAME>.channel.media.azure.net/<LIVE_INGEST_ID>/ingest.isml/eventdata`

For example:

`rtmps://mylivestream.channel.media.azure-test.net:2935/live/0251458ba5df44b2b807ea02f40fed76`

becomes

`https://mylivestream.channel.media.azure-test.net/0251458ba5df44b2b807ea02f40fed76/ingest.isml/eventdata`

### Headers and request body

The HTTP Content-type header **MUST** be set to application/json, so make sure this is set correctly.

```rest
POST /echo/post/json HTTP/1.1
Content-Type: application/json

{

“customJsonName”: “customJsonValue”;

};
```

### Timed metadata limits

| Resource | Default Limit | Per |
| --- | --- | --- |
| Total message body payload size | 256 kb max | Request |
| Requests | 2 | per second  |

## Prerequisites

- A Media Services account
- Familiarity with live streaming from an on-premises encoder. If you haven’t done this before, try live streaming with the [OBS quickstart](live-event-obs-quickstart.md) first. Once you have that setup and running, you should be able to perform the following steps.

## View the sample

The example below shows how a video player catches and displays the timed metadata of the video stream. It uses the Shaka player and its built-in support for [Event Message data (‘emsg’) through the EmsgEvent.](https://shaka-player-demo.appspot.com/docs/api/shaka.Player.html#.event:EmsgEvent)

Media Services also supports the Shaka player ID3 [MetadataEvent](https://shaka-player-demo.appspot.com/docs/api/shaka.Player.html#.event:MetadataEvent), ‘emsg’ events that use the scheme ID uri `https://aomedia.org/emsg/ID3`.

## Review the code on Stackblitz

We've provided a sample Shaka player on Stackblitz for you to work with. Use this button to fork the sample code on Stackblitz.com.

[![Open Fork in StackBlitz](./media/buttons/open_in_stackblitz.svg)](https://stackblitz.com/fork/github/Azure-Samples/media-services-v3-node-tutorials/tree/main/Player/examples/shaka?file=index.html&title=AMS%20Shaka%20Player%20Timed%20Metadata%20Sample)

### Review the HTML page

The *index.html* document contains:

- a div element where the message will show up once it's sent.
- a standard HTML5 video element. Notice that the video element is set to `autoplay` and to `start muted`.
- an input field for the streaming locator URL. There's a placeholder URL in the input field that you can view, but it isn’t a live stream. You'll be replacing this value.

:::code language="html" source="~/../media-services-v3-node-tutorials/Player/examples/shaka/index.html":::

### Review the JavaScript

The *index.js* file creates and manages the player and player events. The `onEventMessage` function is registered to handle the `emsg` event from the Shaka Player and display the messages received from the POST.

`player.addEventListener('emsg', onEventMessage);`

:::code language="javascript" source="~/../media-services-v3-node-tutorials/Player/examples/shaka/index.js" id="EmgHandling" :::

## Create a live event with a streaming locator

If you haven’t done so already with the [OBS quickstart](live-event-obs-quickstart.md)
mentioned earlier, create a live event with a streaming locator.

1. Use the Azure portal, REST or your favorite SDK to create a live event. Copy the *ingest URL* and paste it in a text editor as you'll need to edit it to send a message to the player with an HTTP PUT request.
1. Start the live event and make sure the associated streaming endpoint is also started.

## Stream the live event

Copy and paste the streaming locator into the input field in the player on Stackblitz or optionally update the value on the input element in the index.html file. You should see the live event streaming to the player.

## Create the POST URL

Edit the ingest URL:

1. Change `RTMPS` to `HTTPS`.
1. Remove the port number, including the colon.
1. Remove `/live/` from the path.
1. Append `ingest.isml/eventdata` to the path.

Example:

`rtmps://mylivestream.channel.media.azure-test.net:2935/live/0251458ba5df44b2b807ea02f40fed76`

becomes

`https://mylivestream.channel.media.azure-test.net/0251458ba5df44b2b807ea02f40fed76/ingest.isml/eventdata`

## Create and send a request

You can use any tool or SDK you like for sending an HTTP POST with the metadata in the body to the player.

### Headers and request body

Reminder: The HTTP Content-type header **MUST** be set to application/json. Then, add the information you want to display with the key set as "message". Here is a simple example message:

```http
POST /echo/post/json HTTP/1.1
Content-Type: application/json

{

“message”: “Hello world!”;

};

```

When you send the request, you should see the message in the JSON payload show up in the div floating over the video element.

### Alternative requests

You can send additional information for an interactive overlay. The full setup for that scenario isn’t covered here, but here's what the request body could look like for a quiz. You could iterate through the answers for each "question" (here replacing "message" as the key) and supply a button for the viewer to select.

```http
POST /echo/post/json HTTP/1.1
Content-Type: application/json


{
    "question": "What is the airspeed velocity of an unladen swallow?",
     "answers" : [
        {"a1": "A shrubbery!"},
        {"a2": "I am not a witch!"},
        {"a3":  "An African or European swallow?"},
        {"a4": "It's just a flesh wound."},
    ]
}
```

> [!TIP]
> Open the Developer Tools for the browser and watch the video events that are fired as well as the messages received from the request JSON payload.

### Example POST using cURL

When using cURL, you must set the header using `-H “Content-Type: application/json”`. Use the `-d` flag to set the JSON data on the command line (escape quotes in the JSON body with a backslash when using the command line). Optionally you can point to a JSON file using `-d \@\<path-to-json-file\>`.

A POST is implicit when sending data, so you don't need to use the -X POST flag.

Example POST:

```http
curl https://mylivestream.channel.media.azure.net/618377123f4c49b3937ade20204ca0b2/ingest.isml/eventdata -H "Content-Type: application/json" -d "{\\"message\\":\\"Hello from Seattle\\"}" -v
```

## Clean up resources

Make sure you shut down the live event and the streaming endpoint and delete resources you don’t intend to keep using or you'll be billed.

## Additional information

For more information about the payload and format of timed metadata signals, see [Alliance for Open Media Carriage of ID3 Timed Metadata in the Common Media Application Format (CMAF) specification](https://aomediacodec.github.io/id3-emsg/).
