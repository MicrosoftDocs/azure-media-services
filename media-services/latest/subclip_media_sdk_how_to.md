---
title: How to subclip media with a subclipping job using an SDK
description: You may want your viewers to play only a section of a video. There are a few ways to accomplish this. 1. Use an asset filter to create GOP level accurate clips. 2. Submit subclipping jobs with the standard encoder on an output asset and use the CopyVideo and CopyAudio preset to copy the source audio and video from the top bitrate and generate a single clip. For this example, you will use the subclipping job method using an SDK.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 11/11/2022
ms.author: inhenkel
---

# How to subclip media with a subclipping job using an SDK

You may want your viewers to play only a section of a video. There are a few ways to accomplish this:

1. Use an [asset filter](subclip_media_portal_how_to.md).
1. Submit a subclipping job with the standard encoder on an output asset using REST or an SDK.

For this example, you will use the subclipping job submission method using an SDK.

## Prerequisites

1. Create an output asset. You can either:
    1. Create a live event and a live event output using the [OBS quickstart](live-event-obs-quickstart.md) or your preferred method, or
    1. Upload a media file with a of 5 seconds of video to be omitted at the beginning of the video at the beginning and end of the video and run it through an encoding job. Use the output asset created from the job for this exercise.
1. If using a live event, run your live event for 2 minutes (or so), then stop it. You will be working with the live event output asset.
1. Read the rest of this article.

## SDK example for subclipping

So, say the media’s entire length is 2 minutes or 120 seconds. The beginning shows some pre-production testing that is 5 seconds long and a “Thanks for
watching” animation that is 5 seconds long at the end.

Since you want to exclude the beginning and the end of the video, the values *in between* the beginning and end values are what you will use for the start timestamp (6) and end timestamp (114). To visually represent that:

[0---5\|**6**------------------------------------------------**114**\|115-----120]

## General steps

1. To create a subclipping job, first select the top bitrate video from either an encoding output asset or from a live event output archive asset (also called an archive) by selecting the track by attribute. Use the code found in the [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/81874cae4279841cca7fa591bbfb1a43aa7a4560/VideoEncoding/Encoding_Live_Archive_To_MP4/index.ts) or [Python](https://github.com/Azure-Samples/media-services-v3-python/edit/main/VideoEncoding/EncodingLiveArchiveMP4/encoding-live-archive-to-mp4.py) versions of Encoding a Live Archive to MP4.
1. Add the timestamp beginning and ending ranges to the track selection.

## [Node.JS][#tab/nodejs]

```nodejs
let videoTrackSelection: SelectVideoTrackByAttribute = {
        odataType:"#Microsoft.Media.SelectVideoTrackByAttribute",
        attribute: KnownTrackAttribute.Bitrate,
        filter: KnownAttributeFilter.Top,
        presentationTimeRange: {
            startTimestamp: 60000000,
            endTimestamp: 1140000000,
          }
    }
```

## [Python][#tab/python]

```python

video_track_selection = SelectVideoTrackByAttribute(
  attribute=TrackAttribute.BITRATE,
  filter=AttributeFilter.TOP,
  presentation_time_range=PresentationTimeRange(start_timestamp=60000000, end_timestamp=1140000000)
)

```

---

1. Create a streaming locator for the asset.

## Test the filter

1. Copy the streaming locator URL that is appropriate for your player.
2. Use your player client or the Azure Media Player to test the streaming locator. The video should play only the content from 6 seconds to 115 seconds.

## Try it in the portal

[Subclip media in the Azure portal](subclip_media_portal_how_to.md)
