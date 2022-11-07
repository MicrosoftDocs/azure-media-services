---
title: Signal timed metadata with Azure Media Services
description: Timed metadata is custom data that is inserted into a live stream. Both the data and its insertion timestamp are preserved in the media stream itself. This is so that clients playing the video stream can get the same custom metadata at the exact same time in relation to the video stream. With timed metadata you can add interactivity elements to the live stream such as a poll, add information related to the video content such as speakers, product links, sports player stats, etc. and add metadata about the video such as GPS location, time, etc.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 11/07/2022
ms.author: inhenkel
---

# Timed metadata with Azure Media Services

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
POST https://mylivestream.channel.media.azure-test.net/0251458ba5df44b2b807ea02f40fed76/ingest.isml/eventdata
Content-Type: application/json

{

“message”: “Hello world!”

}
```

### Timed metadata limits

| Resource | Default Limit | Per |
| --- | --- | --- |
| Total message body payload size | 256 kb max | Request |
| Requests | 2 | per second  |

## Sample and how to

To try out signalling timed metadata, see [How to signal timed metadata](stream-signal-timed-metadata-how-to).

## Additional information

For more information about the payload and format of timed metadata signals, see [Alliance for Open Media Carriage of ID3 Timed Metadata in the Common Media Application Format (CMAF) specification](https://aomediacodec.github.io/id3-emsg/).
