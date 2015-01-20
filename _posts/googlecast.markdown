Google Cast:

Google Cast is a technology that enable multi-screen experiences and lets a user send and control content like video from small computing devices.
The sender may be a phone or tablet running on Android or IOS. or it may be a laptop computer running Chrome.

The Chromecast is a low-power device with memory, CPU and GPU limitations, so the receiver application should be as lightweight as possible.

Given the nature of the interaction model, tabs, windows or popups cannot be created in the receiver app, and there should be nothing on the receiver device screen requiring input. all interaction with the application must be done through a send application.

The Cast receiver is a Chrome browser optimized for video playback. as such, WebGL and Chrome Native Client(NACL) are not currently suported, nor are Chrome extensions.

Google Cast supports a single concurrent media stream playback in the audio and video tags or multiple audio tracks using the WebAudio API. Only one video element may be active in the dom at any time. Additional, video sompositing, manipulation, transformations, rotations or zooming ae not supported.
