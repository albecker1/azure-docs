---
title: Spotlight states
titleSuffix: An Azure Communication Services how-to guide
description: Use Azure Communication Services SDKs to send spotlight state.
author: cnwankwo
ms.author: cnwankwo
ms.service: azure-communication-services
ms.subservice: teams-interop
ms.topic: how-to 
ms.date: 03/01/2023
ms.custom: template-how-to
zone_pivot_groups: acs-plat-web-ios-android-windows
---

# Spotlight states
In this article, you learn how to implement Microsoft Teams spotlight capability with Azure Communication Services Calling SDKs. This capability allows users in the call or meeting to pin and unpin videos for everyone. The maximum limit of pinned videos is seven.

Since the video stream resolution of a participant is increased when spotlighted, it should be noted that the settings done on [Video Constraints](../../concepts/voice-video-calling/video-constraints.md) also apply to spotlight.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F). 
- A deployed Communication Services resource. [Create a Communication Services resource](../../quickstarts/create-communication-resource.md).
- A user access token to enable the calling client. For more information, see [Create and manage access tokens](../../quickstarts/identity/access-tokens.md).
- Optional: Complete the quickstart to [add voice calling to your application](../../quickstarts/voice-video-calling/getting-started-with-calling.md)


## Support
The following tables define support for Spotlight in Azure Communication Services.

### Identities & call types
The following table shows support for call and identity types. 

|Identities                                         | Teams meeting | Room | 1:1 call | Group call | 1:1 Teams interop call | Group Teams interop call |
|--------------------------------------|---------------|------|----------|------------|------------------------|--------------------------|
|Communication Services user	| ✔️	          |   ✔️   |          |        ✔️    |	                      |	    ✔️                     |
|Microsoft 365 user	                        | ✔️	          |    ✔️  |          |        ✔️    |                        |        ✔️                  |

### Operations
The following table shows support for individual APIs in Calling SDK to individual identity types. 

|Operations                   | Communication Services user | Microsoft 365 user |
|-----------------------------|------------------------------|-------------------|
| startSpotlight | ✔️ [1] | ✔️ [1] |
| stopSpotlight | ✔️ | ✔️ |
| stopAllSpotlight |  ✔️ [1] | ✔️ [1] | 
| getSpotlightedParticipants |  ✔️ | ✔️ | 

[1] In Teams meeting scenarios, these APIs are only available to users with role organizer, co-organizer, or presenter.

### SDKs
The following table shows support for Spotlight feature in individual Azure Communication Services SDKs.

|  Platforms     | Web | Web UI | iOS | iOS UI | Android | Android UI | Windows |
|---------------|-----|--------|--------|--------|----------|--------|---------|
|Is Supported | ✔️  |  ✔️      |  ✔️      |        |  ✔️        |        |  ✔️       |

::: zone pivot="platform-web"
[!INCLUDE [Spotlight Client-side JavaScript](./includes/spotlight/spotlight-web.md)]
::: zone-end

::: zone pivot="platform-android"
[!INCLUDE [Spotlight Client-side Android](./includes/spotlight/spotlight-android.md)]
::: zone-end

::: zone pivot="platform-ios"
[!INCLUDE [Spotlight Client-side IOS](./includes/spotlight/spotlight-ios.md)]
::: zone-end

::: zone pivot="platform-windows"
[!INCLUDE [Spotlight Client-side Windows](./includes/spotlight/spotlight-windows.md)]
::: zone-end

## Next steps
- [Learn how to manage calls](./manage-calls.md)
- [Learn how to manage video](./manage-video.md)
- [Learn how to record calls](./record-calls.md)
- [Learn how to transcribe calls](./call-transcription.md)
