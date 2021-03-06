
---
title: Record by API
description: How to start recording using API
platform: Linux
updatedAt: Wed Apr 29 2020 08:45:59 GMT+0800 (CST)
---
# Record by API
This page shows how to record a call by calling API methods. You can also record calls by using the command line, see [Record by Command Line](../../en/Recording/recording_cmd_cpp.md). The command line and API methods implement the same recording functions.

> The Agora On-Premise Recording SDK joins a channel as a dummy client. It needs to join the same channel and use the same App ID and channel profile as the Agora Native/Web SDK.

Ensure that you [integrate the SDK](../../en/Recording/recording_integrate_cpp.md) before proceeding.

## Create an instance

```c++
IRecordingEngineEventHandler *handler = <prepare>
	IRecordingEngine* engine = createAgoraRecordingEngine(<APPID>, handler)
```

Call the [`createAgoraRecordingEngine`](https://docs.agora.io/en/Recording/API%20Reference/recording_cpp/classagora_1_1recording_1_1_i_recording_engine.html#a683b055963f285fa0ca63aaab7af27d6) method to create a recording instance and connect it with your app. You can create multiple instances to record simultaneously.


##  Start recording

```c++
RecordingConfig config = {<prepare>}
engine->joinChannel(<channelKey>, <channelId>, <uid>, config)
```

After creating a recording instance, call the [`joinChannel`](https://docs.agora.io/en/Recording/API%20Reference/recording_cpp/classagora_1_1recording_1_1_i_recording_engine.html#a011ff5c4a47816050be60b26ba0fb431) method to join the channel and start recording. In this method, fill in the following parameters:

- `channelKey`: (Optional) The token used in the channel to be recorded. If the channel uses a token, ensure that you pass a token in this parameter. See [Use Security Keys](../../en/Recording/token.md).
- `channelId`: (Mandatory) The name of the channel to be recorded.
- `uid`: (Mandatory) User ID. A 32-bit unsigned integer ranging from 1 to (2<sup>32</sup>-1) that is unique in a channel. If the `uid` is set as 0, the SDK assigns a uid.
- `config`: (Optional) The recording configuration. See [`RecordingConfig`](https://docs.agora.io/en/Recording/API%20Reference/recording_cpp/structagora_1_1recording_1_1_recording_config.html#a511201f4e63f0fae5ef416fb98cb49af) for details. 

After joining the channel, the SDK starts recording when detecting other users in the channel.

If you set [`triggerMode`](https://docs.agora.io/en/Recording/API%20Reference/recording_cpp/namespaceagora_1_1linuxsdk.html#a652d8aefc1931391ff65ae7a088b932f) as `MANUALLY_MODE` in `RecordingConfig`, you need to call the [`startService`](https://docs.agora.io/en/Recording/API%20Reference/recording_cpp/classagora_1_1recording_1_1_i_recording_engine.html#a2d4e78e4164993e64fb0286b9108d478) method to start recording manually. During the recording, you can call the  [`stopService`](https://docs.agora.io/en/Recording/API%20Reference/recording_cpp/classagora_1_1recording_1_1_i_recording_engine.html#a302a83737a67b2693ede181484af862a) method to pause the recording.

```c++
engine->startService()
engine->stopService()
```

> Ensure that you call the `startService` and `stopService` methods only after joining a channel.

## Get the directory of the recording files

```c++
RecordingEngineProperites ps = engine->getProperties()
```

After joining a channel, you can call the [`getProperties`](https://docs.agora.io/en/Recording/API%20Reference/recording_cpp/classagora_1_1recording_1_1_i_recording_engine.html#abf1bcd2dd5a38262ca26e50b3b182f4b) method to get the directory of the recording files.

> You can also get the directory in the [`onUserJoined`](https://docs.agora.io/en/Recording/API%20Reference/recording_cpp/classagora_1_1recording_1_1_i_recording_engine_event_handler.html#a2ca947993a8c8d9ae23fc0545ae1a05d) callback when a remote user joins the channel.

## Stop recording

```c++
engine->leaveChannel()
```

Call the [`leaveChannel`](https://docs.agora.io/en/Recording/API%20Reference/recording_cpp/classagora_1_1recording_1_1_i_recording_engine.html#adafb45815ad0f02dc1c8b3cadb7cd2e3) method to stop recording and leave the channel.

> To start recording again after calling this method, create another instance.

If the [`leaveChannel`](https://docs.agora.io/en/Recording/API%20Reference/recording_cpp/classagora_1_1recording_1_1_i_recording_engine.html#adafb45815ad0f02dc1c8b3cadb7cd2e3) method is not called, the SDK automatically leaves the channel and stops recording when no user is in the channel for more than 300 seconds (you can set this interval by the `idelLimitSec` parameter in `RecordingConfig`) by default.

##  Release resources

```c++
engine->release()
```

Call the [`release`](https://docs.agora.io/en/Recording/API%20Reference/recording_cpp/classagora_1_1recording_1_1_i_recording_engine.html#af4d33159ed8ed249991470e6833d0fd5)  method to destroy the recording instance and release all recording resources.  After releasing the resources, you must create a new instance to use On-premise Recording again. 

> Do not implement the `release` method in the callback thread.

## References
- [Recording file issues](https://docs.agora.io/en/faq/record_file_issue)
- [Recording status issues](https://docs.agora.io/en/faq/record_status_error)
