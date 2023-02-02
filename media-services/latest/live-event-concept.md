---
title: Live events and live outputs concepts
description: This topic provides an overview of live events and live outputs in Azure Media Services v3.
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: conceptual
ms.date: 02/02/2023
ms.author: inhenkel
---
# Media Services live events

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Azure Media Services lets you deliver live events to your customers on the Azure cloud.

> [!TIP]
> If you are migrating from Media Services v2 APIs, the **live event** entity replaces **Channel** in v2 and **live output** replaces **program**.

## Live events

[Live events](/rest/api/media/liveevents) ingest and process live video feeds. When you create a live event, an ingest endpoint is created. The ingest endpoint consumes a live signal from a remote encoder. The remote live encoder sends the feed to the input endpoint using either the [RTMP](https://helpx.adobe.com/adobe-media-server/dev/stream-live-media-rtmp.html) or [Smooth Streaming](/openspecs/windows_protocols/ms-sstr/8383f27f-7efe-4c60-832a-387274457251) (fragmented-MP4) input protocol. For the RTMP ingest protocol, the content can be sent in the clear (`rtmp://`) or securely encrypted on the wire(`rtmps://`). For the Smooth Streaming ingest protocol, the supported URL schemes are `http://` or `https://`.

The default allocation is 5 live events per Media Services account. If you would like to increase this limit, please file a support ticket in the Azure portal.

## Live event types

A [live event](/rest/api/media/liveevents) can be set to either a basic or standard *pass-through* or *live encoding*. The types are set during creation using the live event encoding type.

* **Passthrough basic**: An on-premises live encoder sends a multiple bitrate stream. The basic pass-through is limited to a peak ingress of 5 Mbps, 8-hour DVR window, and live transcription is not supported.
* **Passthrough standard**: An on-premises live encoder sends a multiple bitrate stream. The standard pass-through has higher ingest limits, 25-hour DVR window, and support for live transcriptions.
* **Standard**: An on-premises live encoder sends a single bitrate stream to the live event and Media Services creates multiple bitrate streams. If the contribution feed is of 720p or higher resolution, the **Default720p** preset will encode a set of 6 resolution/bitrates pairs.
* **Premium 1080p**: An on-premises live encoder sends a single bitrate stream to the live event and Media Services creates multiple bitrate streams. The Default1080p preset specifies the output set of resolution/bitrates pairs.

> [!NOTE]
> The max framerate is 30 fps for both Standard and Premium encoding.

## Pass-through live event

When using the basic or standard pass-through **live event**, you use your on-premises live encoder to generate a multiple bitrate video stream and send that to the live event (using RTMP or fragmented-MP4 protocol). The live event then carries through the incoming video streams without any further processing. A pass-through live event is optimized for long-running live events or 24x365 linear live streaming. When creating this type of live event, specify pass-through "basic" or "standard".

You can send the feed at resolutions up to 4K and at a frame rate of 60 frames/second, with either H.264/AVC or H.265/HEVC (Smooth ingest only) video codecs, and AAC (AAC-LC, HE-AACv1, or HE-AACv2) audio codec. For more information, see [Live event types comparison](live-event-types-comparison-reference.md).

> [!NOTE]
> Using a pass-through method is the most economical way to do live streaming when you're doing multiple events over a long period of time, and you have already invested in on-premises encoders. See [Pricing](https://azure.microsoft.com/pricing/details/media-services/) details.
>

## Live encoding live event

When using live encoding, you configure your on-premises live encoder to send a single bitrate video to the live event (using RTMP or Fragmented-Mp4 protocol). You then set up a live event so that it encodes the incoming single bitrate stream to a multiple bitrate video stream. This makes the output available for delivery to play back devices via protocols like MPEG-DASH, HLS, and Smooth Streaming.

In this case, you can send the contribution feed only at resolutions up to 1080p resolution at a frame rate of 30 frames/second, with H.264/AVC video codec and AAC (AAC-LC, HE-AACv1, or HE-AACv2) audio codec. For more information, see [Live event types comparison](live-event-types-comparison-reference.md).

### Low Latency HLS and DASH streaming options

For details on how to achieve low latency with live event encoding see the [Low Latency HLS (LL-HLS) and DASH streaming options](live-event-latency-reference.md) and the [Live streaming best practices guide](live-event-streaming-best-practices-guide.md).

### Live encoding output resolution and bitrates

The resolutions and bitrates in the resulting output from the live encoder is determined by the preset:

* When you use the **Standard** live encoder, the *Default720p* preset specifies a set of six resolution/bit rate pairs, going from 720p at 3.5 Mbps down to 192p at 200 kbps.
* When you use a **Premium1080p** live encoder, the *Default1080p* preset specifies a set of six resolution/bit rate pairs, going from 1080p at 3.5 Mbps down to 180p at 200 kbps.

For information, see [System presets](live-event-types-comparison-reference.md#system-presets).

> [!NOTE]
> If you need to customize the live encoding preset, please open a support ticket via Azure Portal. You should specify the desired table of video resolution/bitrates and audio bitrates. For video, verify that there is only one layer at 720p, and at most 6 layers for video. For audio, you can customize with the following discrete AAC audio bitrates (96k, 112k, 128k, 160k, 192k, 224k, 256k, 320k, 384k, 448k, 512k). Multiple audio tracks at different bitrates are allowed and can be included in the custom preset.  Also please specify that you are requesting a *custom* preset in the support ticket.

See the REST API for [LiveEventEncodingType](/rest/api/media/liveevents/create#liveeventencodingtype) or the [.Net](/dotnet/api/microsoft.azure.management.media.liveeventsoperationsextensions?view=azure-dotnet&preserve-view=true), [Node.JS](/python/api/azure-mgmt-media/azure.mgmt.media.operations.liveeventsoperations?view=azure-python&preserve-view=true) or [Python](/python/api/azure-mgmt-media/azure.mgmt.media.operations.liveeventsoperations?view=azure-python&preserve-view=true) SDKs.  Additionally, you can try the [Live Event sample code](samples-live-event-reference.md).

## Live event options

When creating a live event, you can specify the following options:

* **Name** and **description**.
* For Standard and Premium encoding, you can choose the **stretch mode** of the encoded video:
  * **None**: Strictly respects the output resolution specified in the encoding preset without considering the pixel aspect ratio or display aspect ratio of the input video.
  * **AutoSize**:  Overrides the output resolution and changes it to match the display aspect ratio of the input, without padding. For example, if the input is 1920x1080 and the encoding preset asks for 1280x1280, then the value in the preset is overridden, and the output will be at 1280x720, which maintains the input aspect ratio of 16:9.
  * **AutoFit**: Pads the output (with either letterbox or pillar box) to honor the output resolution, while ensuring that the active video region in the output has the same aspect ratio as the input. For example, if the input is 1920x1080 and the encoding preset asks for 1280x1280, then the output will be at 1280x1280, which contains an inner rectangle of 1280x720 at aspect ratio of 16:9, with pillar box regions 280 pixels wide at the left and right.
* **Streaming protocol** RTMP or Smooth streaming. Note: You can't change the protocol option while the live event or its associated live outputs are running. If you require different protocols, create a separate live event for each streaming protocol.
* **Input ID** which is a globally unique identifier for the live event input stream.
* **Static hostname prefix** which includes none (in which case a random 128 bit hex string will be used), Use live event name, or Use custom name.  When you choose to use a customer name, this value is the Custom hostname prefix.
* **Input key frame interval**, which is the duration (in seconds) of each media segment in the HLS output. The value should be a non-zero integer in the range of 0.5 to 20 seconds.  The value defaults to 2 seconds if *neither* of the input or output key frame intervals are set. The key frame interval is only allowed on pass-through events.
* **Autostart**. When autostart is set to true, the live event will be started after creation. The billing starts as soon as the live event starts running. You must explicitly stop the live event to halt further billing. Alternatively, you can start the event when you're ready to start streaming.
* **IP restrictions** on the ingest and preview. You can define the IP addresses that are allowed to ingest a video to this live event. Allowed IP addresses can be specified as either a single IP address (for example '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using an IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.252.0)').
    * If no IP addresses are specified and there's no rule definition, then no IP address will be allowed. To allow any IP address, create a rule and set 0.0.0.0/0. The IP addresses have to be in one of the following formats: IpV4 or IPv6 addresses with four numbers or CIDR address range. For more information about using IPv4 or IPv6, see [Restrict access to DRM license and AES key delivery using IP allowlists](drm-content-protection-key-delivery-ip-allow.md).
    * If you want to enable certain IPs on your own firewalls or want to constrain inputs to your live events to Azure IP addresses, download a JSON file from [Azure Datacenter IP address ranges](https://www.microsoft.com/download/details.aspx?id=41653). For details about this file, select the **Details** section on the page.
* **Live transcription** which is disabled by default. For more information about live transcription read [Live transcription](live-event-live-transcription-how-to.md).

## StandBy mode

When you create a live event, you can set it to StandBy mode. While the event is in StandBy mode, you can edit the description and the static hostname prefix as well as restrict input and preview access settings.  StandBy mode is still a billable mode, but is priced differently than when you start a live stream.

For more information, see [Live event states and billing](live-event-states-billing-concept.md).

## Live outputs

Once you have set up a stream from an on-premises encoder to a live event, you can begin the streaming event by creating an [Asset](/rest/api/media/assets), [live output](/rest/api/media/liveoutputs), and [Streaming Locator](/rest/api/media/streaminglocators). Live output will archive the stream and make it available to viewers through the [Streaming Endpoint](/rest/api/media/streamingendpoints).

## Live event output questions

See the [live event questions in the FAQ](frequently-asked-questions.yml). For information on live event quotas, see [quotas and limits](limits-quotas-constraints-reference.md)

## More details about setting up live events

### Naming rules

* Max live event name is 32 characters.
* The name should follow this [regex](/dotnet/standard/base-types/regular-expression-language-quick-reference) pattern: `^[a-zA-Z0-9]+(-*[a-zA-Z0-9])*$`.

Also see [Streaming Endpoints naming conventions](stream-streaming-endpoint-concept.md#naming-convention).

> [!TIP]
> To guarantee uniqueness of your live event name, you can generate a GUID then remove all the hyphens and curly brackets (if any). The string will be unique across all live events and its length is guaranteed to be 32.

### Live event ingest URLs

Once the live event is created, you can get ingest URLs that you'll provide to the live on-premises encoder. The live encoder uses these URLs to input a live stream. For more information, see [Recommended on-premises live encoders](encode-recommended-on-premises-live-encoders.md).

>[!NOTE]
> As of the 2020-05-01 API release, "vanity" URLs are known as Static Host Names (useStaticHostname: true)


> [!NOTE]
> For an ingest URL to be static and predictable for use in a hardware encoder setup, set the **useStaticHostname** property to true and set the **accessToken** property to the same GUID on each creation.

* Non static hostname

    A non static hostname is the default mode in Media Services v3 when creating a **LiveEvent**. You can get the live event allocated slightly more quickly, but the ingest URL that you would need for your live encoding hardware or software will be randomized . The URL will change if you do stop/start the live event. Non static hostnames are only useful in scenarios where an end user wants to stream using an app that needs to get a live event very quickly and having a dynamic ingest URL isn't a problem.

    If a client app doesn't need to pre-generate an ingest URL before the live event is created, let Media Services auto-generate the Access Token for the live event.

* Static Hostnames

    Static hostname mode is preferred by most operators that wish to pre-configure their live encoding hardware or software with an RTMP ingest URL that never changes on creation or stop/start of a specific live event. These operators want a predictive RTMP ingest URL which doesn't change over time. This is also very useful when you need to push a static RTMP ingest URL into the configuration settings of a hardware encoding device like the BlackMagic Atem Mini Pro, or similar hardware encoding and production tools.

    > [!NOTE]
    > In the Azure portal, the static hostname URL is called "*Static hostname prefix*".

    To specify this mode in the API, set `useStaticHostName` to `true` at creation time (default is `false`). When `useStaticHostname` is set to true, the `hostnamePrefix` specifies the first part of the hostname assigned to the live event preview and ingest endpoints. The final hostname would be a combination of this prefix, the media service account name and a short code for the Azure Media Services data center.

    To avoid a random token in the URL, you also need to pass your own access token (`LiveEventInput.accessToken`) at creation time.  The access token has to be a valid GUID string (with or without the hyphens). Once the mode is set, it can't be updated.

    The access token must be unique for the Azure region and for the Media Services account. If your app needs to use a static hostname ingest URL, you are encouraged to always create fresh GUID instance for use with a specific combination of region, media services account, and live event.

    Use the following APIs to enable the static hostname URL and set the access token to a valid GUID (for example, `"accessToken": "1fce2e4b-fb15-4718-8adc-68c6eb4c26a7"`).

    |Language|Enable static hostname URL|Set access token|
    |---|---|---|
    |REST|[properties.useStaticHostname](/rest/api/media/liveevents/create#liveevent)|[LiveEventInput.useStaticHostname](/rest/api/media/liveevents/create#liveeventinput)|
    |CLI|[--use-static-hostname](/cli/azure/ams/live-event#az_ams_live_event_create)|[--access-token](/cli/azure/ams/live-event#optional-parameters)|
    |.NET|[LiveEvent.useStaticHostname](/dotnet/api/microsoft.azure.management.media.models.liveevent.usestatichostname?view=azure-dotnet&preserve-view=true#Microsoft_Azure_Management_Media_Models_LiveEvent_UseStaticHostname)|[LiveEventInput.AccessToken](/dotnet/api/microsoft.azure.management.media.models.liveeventinput.accesstoken#Microsoft_Azure_Management_Media_Models_LiveEventInput_AccessToken)|

### Live ingest URL naming rules

* The *random* string below is a 128-bit hex number (which is composed of 32 characters of 0-9 a-f).
* *your access token*: The valid GUID string you set when using the static hostname setting. For example, `"1fce2e4b-fb15-4718-8adc-68c6eb4c26a7"`.
* *stream name*: Indicates the stream name for a specific connection. The stream name value is usually added by the live encoder you use. You can configure the live encoder to use any name to describe the connection, for example: "video1_audio1", "video2_audio1", "stream".

> [!WARNING]
> If you use any special characters or spaces in the name of your stream, your live ingest will fail. See Media Services resource [naming conventions](media-services-apis-overview.md#naming-conventions) in the developer concepts overview.

#### Non-static hostname ingest URL

##### RTMP

`rtmp://<random 128bit hex string>.channel.media.azure.net:1935/live/<auto-generated access token>/<stream name>`<br/>
`rtmp://<random 128bit hex string>.channel.media.azure.net:1936/live/<auto-generated access token>/<stream name>`<br/>
`rtmps://<random 128bit hex string>.channel.media.azure.net:2935/live/<auto-generated access token>/<stream name>`<br/>
`rtmps://<random 128bit hex string>.channel.media.azure.net:2936/live/<auto-generated access token>/<stream name>`<br/>

##### Smooth streaming

`http://<random 128bit hex string>.channel.media.azure.net/<auto-generated access token>/ingest.isml/streams(<stream name>)`<br/>
`https://<random 128bit hex string>.channel.media.azure.net/<auto-generated access token>/ingest.isml/streams(<stream name>)`<br/>

#### Static hostname ingest URL

In the following paths, `<live-event-name>` means either the name given to the event or the custom name used in the creation of the live event.

##### RTMP

`rtmp://<live event name>-<ams account name>-<region abbrev name>.channel.media.azure.net:1935/live/<your access token>/<stream name>`<br/>
`rtmp://<live event name>-<ams account name>-<region abbrev name>.channel.media.azure.net:1936/live/<your access token>/<stream name>`<br/>
`rtmps://<live event name>-<ams account name>-<region abbrev name>.channel.media.azure.net:2935/live/<your access token>/<stream name>`<br/>
`rtmps://<live event name>-<ams account name>-<region abbrev name>.channel.media.azure.net:2936/live/<your access token>/<stream name>`<br/>

##### Smooth streaming

`http://<live event name>-<ams account name>-<region abbrev name>.channel.media.azure.net/<your access token>/ingest.isml/streams(<stream name>)`<br/>
`https://<live event name>-<ams account name>-<region abbrev name>.channel.media.azure.net/<your access token>/ingest.isml/streams(<stream name>)`<br/>

## Live event preview URL

Once the live event starts receiving the contribution feed, you can use its preview endpoint to preview and validate that you're receiving the live stream before further publishing. After you've checked that the preview stream is good, you can use the live event to make the live stream available for delivery through one or more (pre-created) Streaming Endpoints. To accomplish this, create a new [live output](/rest/api/media/liveoutputs) on the live event.

> [!IMPORTANT]
> Make sure that the video is flowing to the preview URL before continuing!

## Live event long-running operations

For details, see [long-running operations](media-services-apis-overview.md#long-running-operations).

[!INCLUDE [media-services-community](includes/media-services-community.md)]
