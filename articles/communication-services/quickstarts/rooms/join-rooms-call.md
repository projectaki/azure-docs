---
title: Quickstart - Join a room call
titleSuffix: An Azure Communication Services quickstart
description: In this quickstart, you'll learn how to join a room call using web or native mobile calling SDKs
services: azure-communication-services
author: radubulboaca
manager: mariusu

ms.author: radubulboaca
ms.date: 07/27/2022
ms.topic: quickstart
ms.service: azure-communication-services
ms.custom: mode-other
zone_pivot_groups: acs-web-ios-android
---

# Quickstart: Join a room call

[!INCLUDE [Public Preview Notice](../../includes/public-preview-include.md)]

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- An active Communication Services resource and connection string. [Create a Communication Services resource](../create-communication-resource.md).
- Two or more Communication User Identities. [Create and manage access tokens](../access-tokens.md) or [Quick-create identities for testing](../identity/quick-create-identity.md).
- A room resource. [Create and manage rooms](get-started-rooms.md)

## Obtain user access token

You'll need to create a User Access Token for each call participant. [Learn how to create and manage user access tokens](../access-tokens.md). You can also use the Azure CLI and run the command below with your connection string to create a user and an access token.

```azurecli-interactive
az communication identity token issue --scope voip --connection-string "yourConnectionString"
```

For details, see [Use Azure CLI to Create and Manage Access Tokens](../access-tokens.md?pivots=platform-azcli).

::: zone pivot="platform-web"
[!INCLUDE [Join a room call from web calling SDK](./includes/rooms-quickstart-call-web.md)]
::: zone-end

::: zone pivot="platform-ios"
[!INCLUDE [Join a room call from iOS calling SDK](./includes/rooms-quickstart-call-ios.md)]
::: zone-end

::: zone pivot="platform-android"
[!INCLUDE [Join a room call from Android calling SDK](./includes/rooms-quickstart-call-android.md)]
::: zone-end

## Next steps 

In this section you learned how to:
> [!div class="checklist"]
> - Add video calling to your application
> - Pass the room identifier to the calling SDK
> - Join a room call from your application

You may also want to:
 - Learn about [rooms concept](../../concepts/rooms/room-concept.md)
 - Learn about [voice and video calling concepts](../../concepts/voice-video-calling/about-call-types.md)
 - Learn about [authentication concepts](../../concepts/authentication.md)