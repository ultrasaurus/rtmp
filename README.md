# Real Time Messaging Protocol Overview

Real Time Messaging Protocol (RTMP) supports one or more audio, video and data streams, as well as system and user-defined command messages. The protocol was designed to support very low-latency for interactive, multiparty applications with seamless integration of live or recorded video, as well as broadcast streaming, video on demand (VOD) use cases.

RTMP supports multiple transports:
* TCP/IP, optionally with secure socket connection
* HTTP/S
* UDP via [RTMFP](https://tools.ietf.org/html/rfc7425)

### Connect

1. Handshake (5.2)
2. Client Command Message: Connect
3. Bandwidth Coordination
4. Server Message: StreamBegin
5. Server Command Response: Connect success/failure

### Command Messages

<TODO>

### Multiplexed Streams

After handshaking, the connection multiplexes one or more streams. Each stream is a logical channel, carrying messages of one type for a single audio, video or data stream.

The protocol supports multiple synchronized audio, video and data streams; however some client or server implementations may limit the number or type of streams.

#### Example use case
A simple use case of audio-video streaming could include one audio stream and one video stream. The protocol enables each stream to be multiplexed such that small high frequency audio messages may be interleaved through multiple chunks representing a larger video frame. This stream construction allows a low-power client to prioritize audio playback and drop video data. For example, in the case of a device without hardware decompression, this allows using CPU for other operations infrequent operations without dropping audio which is typically more disruptive for a human audience.

#### RTMP Chunk Stream

When using a reliable, ordered transport protocol, such as TCP/IP, RTMP allows for low-latecy, interactive application by splitting larger messages into smaller "chunks" for multiplexed delivery.

Chunking allows small messages to be sent with less overhead, as the chunk header contains a compressed representation of information that would otherwise have to be included in the message itself.


