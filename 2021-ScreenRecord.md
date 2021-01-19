## Brief
Record the entire screen using [Screencast](https://knowledge.autodesk.com/community/screencast). 

Fusion 360 a software wants to allow its users to record screens online and standalone.

What problems you'd have to solve to match the initial app:

## Problem
Input: Capture each screen frame from the screen

## Solution
1. Screencapture API can be used to solve this.

2. Navigator has options in the browser to allow to capture specific windows.

```
    let displayMediaOptions = {video: true, audio: true } //can configure based on user inputs
    window.navigator.mediaDevices.getDisplayMedia(displayMediaOptions).then((stream) => {
        //record this mediastream
    })
```


## Problem
Input: Capture audio from microphone

## Solution
1. If you implement the above solution, you don't need to separate audio input you can record that along with the video.

```
    let displayMediaOptions = { video: true, audio: true} //set audio to true to do that
    window.navigator.mediaDevices.getDisplayMedia(displayMediaOptions)
```

## Problem
System: Capturing specific window while using Navigator

## Solution


## Problem
Input: Capture all keystrokes in the input

## Solution
1. You can add event listener to get the keystrokes.

```
function printKeyPressed(e) {
    console.log(e.code)
}

//When the record button is pressed
document.addEventListener('keydown',printKeyPressed,true);

//When the record button is stopped
document.removeEventListener('keydown',printKeyPressed, true);
```
Used some event listeners in [LuxuryPresence](2017-Luxurypresence.md) for `animationstart` and `animationend` of carousels


## Problem
Output: Display keystrokes in the video

## Solution
1. While capturing keystrokes we can also save the time diff in seconds: 

```
[
    {
        keystroke: 'CMD',
        time: '00:01' //time from when the recording started
    }
]
```

2. Once all frames are captured from mediastream, you render over each frame using canva

![Keycapture](https://i.stack.imgur.com/LzRMn.png)

This is something I was able to do in the [thumbnail editor](2021-YoutubeThumbnailMaker.md)

3. You can use `canvas` from html5 to do this (not sure about the implementation, but it is possible)

## Problem
Input: Capture video from camera

## Solution
1. Solved with `Navigator` `getDisplayMedia` options

## Problem
Output: Combine all frames and present the viewer

## Solution


## Problem
Output: Allow the user to edit the frames to remove or add any section

## Solution


