---
title: How to subclip media
description: You may want your viewers to play only a section of a video. There are a couple of ways to accomplish this. - Use an asset filter. - Submit subclipping jobs with the standard encoder on an output asset using an SDK.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: how-to
ms.date: 11/16/2022
ms.author: inhenkel
---

# How to subclip media

You may want your viewers to play only a section of a video. There are a couple ways to accomplish this:

1. Use an asset filter.
1. Submit subclipping jobs with the standard encoder on an output asset using an SDK.

## Prerequisites

For using an asset filter:

- Read the [Filters](/azure/media-services/latest/filters-concept) article to understand what filters are.
- Read [Filter your manifests using Dynamic Packager](/azure/media-services/latest/filters-dynamic-manifest-concept) to understand:
  - Dynamic Manifests
  - [URLs with filters in the query string](filters-dynamic-manifest-concept.md#examples-urls-with-filters-in-query-string)
  - [Rendition filtering](filters-dynamic-manifest-concept.md#rendition-filtering)
  - [Creating subclips (views) from a live archive](filters-dynamic-manifest-concept.md#creating-subclips-views-from-a-live-archive)

For setting up the output asset:

1. Create an output asset. You can either:
    1. Create a live event and a live event output using the [OBS quickstart](live-event-obs-quickstart.md) or your preferred method, or
    1. Upload a media file with a of 5 seconds of video to be omitted at the beginning of the video at the beginning and end of the video and run it through an encoding job. Use the output asset created from the job for this exercise.
1. If using a live event, run your live event for 2 minutes (or so), then stop it. You will be working with the live event output asset.
1. Read the rest of this article.

## Asset filter example

You can use the portal to create an asset filter to limit the content presented to your viewers. For this example, you are going to use one filter to filter out segments of time at the *beginning* and *end* of the video.

So, say the media’s entire length is 2 minutes or 120 seconds. The beginning shows some pre-production testing that is 5 seconds long and a “Thanks for
watching” animation that is 5 seconds long at the end.

Since you want to exclude the beginning and the end of the video, the values *in between* the beginning and end values are what you will use for the start timestamp (6) and end timestamp (114).

### Create an asset filter in the portal

1. Sign into the portal.
2. Navigate to the Media Services account you are working with.
3. Select **Assets**.
4. Select the **output asset** for your live event.
5. Select **Add an asset filter**. The asset filter screen will appear.
6. In the Asset filter name field, enter a name for your asset filter. Use something like *5offbegend* to remind yourself of what the filter is delivering to viewers.
7. In the **Timescale** field, change the value to 1.
8. In the **Start timestamp** field, enter the start timestamp of *0*.
9. In the **End timestamp** field, enter 114.
10. Select **Save**. The filter will appear in the **Asset filters** list.

### Create a streaming locator

Your player client will use the filter in the query string of the request for the asset. To create that URL, create a streaming locator.

1. One the same screen, select **+ New streaming locator**. The streaming locator screen will appear.
2. In the **Name field**, change the streaming locator name to *5offbegend-loc* or something that tells you which filter was used for the streaming locator.
3. From the **Filters** dropdown list, select the filter you just created.
4. Select **Add**. The filter will be used when the streaming locator is requested by the player client.

## Test the filter

1. Copy or GET the streaming locator URL that is appropriate for your player.
2. Use your player client or the Azure Media Player to test the streaming locator. The video should play only the content from 6 seconds to 115 seconds.

<hr>

## SDK example

1. To create a subclipping job, first select the top bitrate video from either an encoding output asset or from a live event output archive asset (also called an archive) by selecting the track by attribute. Use the code found in the [Node.JS](https://github.com/Azure-Samples/media-services-v3-node-tutorials/blob/81874cae4279841cca7fa591bbfb1a43aa7a4560/VideoEncoding/Encoding_Live_Archive_To_MP4/index.ts) or [Python](https://github.com/Azure-Samples/media-services-v3-python/edit/main/VideoEncoding/EncodingLiveArchiveMP4/encoding-live-archive-to-mp4.py) versions of Encoding a Live Archive to MP4.
2. Add the timestamp beginning and ending ranges to the track selection.

#### [Node.JS](#tab/node)

:::code language="nodejs" source="~/../media-services-v3-node-tutorials/VideoEncoding/Encoding_Live_Archive_To_MP4/index.ts" id="TopBitRate":::

:::code language="nodejs" source="~/../media-services-v3-node-tutorials/VideoEncoding/Encoding_Live_Archive_To_MP4/index.ts" id="SubclipJobInput":::

#### [Python](#tab/python)

:::code language="python" source="~/../media-services-v3-python/VideoEncoding/EncodingLiveArchiveMP4/encoding-live-archive-to-mp4.py" id="TopBitRate":::

:::code language="python" source="~/../media-services-v3-python/VideoEncoding/EncodingLiveArchiveMP4/encoding-live-archive-to-mp4.py" id="SubclipJobInput":::

---

3. Once the job is complete, create a streaming locator for the output asset, get the URL appropriate for your player client and test it.
