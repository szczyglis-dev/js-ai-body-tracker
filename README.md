Javascript, current release: **1.0.0** build 2022-07-20

# JS AI BODY TRACKER - tracker.js

**JS AI Body Tracker `(tracker.js)` is a library that implements machine learning-based models for image recognition and human movement analysis. Library is written in javascript, it doesn't require node.js. It supports 3 different models for detecting the human position on the video: `MoveNet`, `PoseNet` and `BlazePose`. Package offers real-time image analysis from three different image sources: web or smartphone camera, video files and online streaming (IPTV/m3u8).**

More information about implemented neural networks: 
https://github.com/tensorflow/tfjs-models/tree/master/pose-detection

## Features:

- easy to implement in your own JS application
- works in real-time directly in webbrowser
- support for 3 different image sources: web camera, video files (mp4, mkv, avi, webm) and online stream (IPTV / m3u8)
- 3 models of neural networks: `MoveNet`, `PoseNet`, `BlazePose`
- real-time 3D mapping
- can be easily extended with events / hooks
- only one file, for direct import in your own application, no node.js required
- uses `TensorFlow JS`, `ScatterGL` and `videoJS` libraries

Detecting human pose in MP4 video in real-time:

![gif1](https://user-images.githubusercontent.com/61396542/180048048-ebd4fdbe-9b0e-43a8-b34a-255bd092e366.gif)
![gif2](https://user-images.githubusercontent.com/61396542/180047990-523f6706-1241-4cd6-9114-8e1e887cce7f.gif)

Detecting human pose in online IPTV/m3u8 stream in real-time:

![gif3](https://user-images.githubusercontent.com/61396542/180048146-80cf69b3-26ac-4841-bbe5-7c16cc757491.gif)


## Online demo

A demo of a real-time working sample application using the library is here:
## https://szczyglis.dev/js-ai-body-tracker


There are 3 input video sources available in the demo application: camera, video film and IPTV / m3u8 stream. 
The entire process of image analysis takes place in real-time.

## Basic usage:

```js
// javascript

tracker.setModel('MoveNetSinglePoseLightning'); // define model to use

tracker.el3D = '#view_3d'; // define HTML container 
tracker.elCanvas = '#canvas'; // define HTML canvas container
tracker.elVideo = '#video'; // define HTML video container

tracker.run('camera'); // run
```
The repository includes a sample application illustrating the operation and use of the library.

## Usage step by step

First, you need to define two HTML elements: video and canvas:

```html
<canvas id="canvas"></canvas>
<video id="video"></video>
```
Then you need to import the library and configure it:

```html
<script src="./js/tracker.js"></script>
<script>
	tracker.setModel('MoveNetSinglePoseLightning');	
	tracker.elCanvas = '#canvas';
	tracker.elVideo = '#video';
	tracker.el3D = '#view_3d';
	tracker.run('camera');
</script>
```

### Examples of use

**1) VIDEO INPUT: webcam / smartphone camera**

```html
<!DOCTYPE html>
<html>
<head>
</head>
<body>
<div class="container">
	<canvas id="canvas" width="500" height="500"></canvas>
	<video id="video" width="500" height="500" style="display:none">
		<source src="">
	</video>				
</div>

<!-- Load Tensor Flow -->
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-core"></script>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-converter"></script>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-backend-webgl"></script>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/pose-detection"></script>

<!-- Load three.js -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js"></script>
<!-- Load scatter-gl.js -->
<script src="https://cdn.jsdelivr.net/npm/scatter-gl@0.0.13/lib/scatter-gl.min.js"></script>

<!-- Load tracker.js -->
<script src="./js/tracker.js"></script>
<script>
	tracker.setModel('MoveNetSinglePoseLightning');
	tracker.elCanvas = '#canvas';
	tracker.elVideo = '#video';
	tracker.run('camera');
</script>
</body>
</html>
```
The above code activates the camera and initializes the model detecting the human position, and then displays the points detected on the video from camera on the canvas element.

**2) VIDEO INPUT: movie file (mp4, mkv, webp)**

```html
<!DOCTYPE html>
<html>
<head>
</head>
<body>
<div class="container">
	<canvas id="canvas" width="500" height="500"></canvas>
	<video id="video" width="500" height="500" style="display:none">
		<source src="movie.mp4">
	</video>				
</div>

<!-- Load Tensor Flow -->
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-core"></script>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-converter"></script>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-backend-webgl"></script>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/pose-detection"></script>

<!-- Load three.js -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js"></script>
<!-- Load scatter-gl.js -->
<script src="https://cdn.jsdelivr.net/npm/scatter-gl@0.0.13/lib/scatter-gl.min.js"></script>

<!-- Load tracker.js -->
<script src="./js/tracker.js"></script>
<script>
	tracker.setModel('MoveNetSinglePoseLightning');
	tracker.elCanvas = '#canvas';
	tracker.elVideo = '#video';
	tracker.run('video');
</script>
</body>
</html>
```
The above code loads the movie `movie.mp4` and initializes the human position analysis model, then displays the points detected on the video in real time, superimposing them on the input video.

**3) VIDEO INPUT: online stream (IPTV/m3u8)**

```html
<!DOCTYPE html>
<html>
<head>
	<link href="https://cdnjs.cloudflare.com/ajax/libs/video.js/7.0.0/video-js.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/video.js/7.0.0/video.min.js"></script>
</head>
<body>
<div class="container">
	<canvas id="canvas" width="500" height="500"></canvas>
	<video id="video" class="video-js vjs-fluid vjs-default-skin" preload="metadata" width="500" height="500" style="display:none">
		<source src="https://multiplatform-f.akamaihd.net/i/multi/will/bunny/big_buck_bunny_,640x360_400,640x360_700,640x360_1000,950x540_1500,.f4v.csmil/master.m3u8">
	</video>				
</div>

<!-- Load Tensor Flow -->
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-core"></script>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-converter"></script>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs-backend-webgl"></script>
<script src="https://cdn.jsdelivr.net/npm/@tensorflow-models/pose-detection"></script>

<!-- Load three.js -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js"></script>
<!-- Load scatter-gl.js -->
<script src="https://cdn.jsdelivr.net/npm/scatter-gl@0.0.13/lib/scatter-gl.min.js"></script>

<!-- Load tracker.js -->
<script src="./js/tracker.js"></script>
<script>
	tracker.setModel('MoveNetMultiPoseLightning');
	tracker.elCanvas = '#canvas';
	tracker.elVideo = '#video';
	tracker.run('stream');
</script>
</body>
</html>
```
The above code opens .m3u8 online video stream and initiates the detection model the position of the human, and then displays the points detected in the image in the canvas element superimposed on the stream image. **Note that the videoJS library is used to handle the stream.**


### Configuration

**Model**

The library has preconfigured settings for 3 different neural network models, you can use these settings or define all options manually. To use the predefined model, use the `setModel()` method:

```js
tracker.setModel('MoveNetSinglePoseLightning');
```

**Available models:**

- `MoveNetSinglePoseLightning`			
- `MoveNetSinglePoseThunder`
- `MoveNetMultiPoseLightning`
- `PoseNetMobileNetV1`
- `PoseNetResNet50`
- `BlazePoseLite`
- `BlazePoseHeavy`
- `BlazePoseFull`

You can also define the settings manually, e.g. MoveNet network and the "multipose" settings:

```js
tracker.detectorModel = poseDetection.SupportedModels.MoveNet;
tracker.detectorConfig = {
    modelType: poseDetection.movenet.modelType.MULTIPOSE_LIGHTNING,
    enableSmoothing: true,
    multiPoseMaxDimension: 256,
    enableTracking: true,
    trackerType: poseDetection.TrackerType.BoundingBox
}
tracker.minScore = 0.35;
```
Network models differ in efficiency and accuracy, you can read more about the models of these neural networks on the Google website:

https://github.com/tensorflow/tfjs-models/tree/master/pose-detection


**Input video source**

You can define 3 different video sources:

- `camera`
- `video`
- `stream`

To select a source, call the method `run()` with the name of the source as argument, e.g .:

```js
tracker.run('camera') // takes video from webcam
```
```js
tracker.run('video') // takes video from movie file (e.g. mp4)
```
```js
tracker.run('stream') // takes video from m3u8 online stream
```

**HTML elements configuration**

You need to define elements for video, canvas and for 3D output (only available for BlazePose model). To do this, set the appropriate values:

```js
tracker.elCanvas = '#canvas';
tracker.elVideo = '#video';
tracker.el3D = '#view_3d';
```

**Display settings**

You can define the size of points displayed on the image:

```js
tracker.pointWidth = 6; // points connection width
tracker.pointRadius = 8; // point circle radius
```

**Events / hooks**

You can define your own functions that will handle, for example, points in the image detected by the neural network, the event / hook system is used for this. To define a hook, use the `on` method. For example, to define a Hook that will display all detected points in real-time live, write the following code:

```js
tracker.on('beforeupdate', function(poses) {
	console.log(poses);
});
````

The above code will make the console display a set of points detected in the image when rendering each frame.

You can define hooks for 4 types of events:

`beforeupdate` - hook executes before canvas render in every frame

`afterupdate` - hook executes after canvas render in every frame

`statuschange` - hook executes when status was changed

`detectorerror` - hook executes when detector error occured

`videoerror` - hook executes when video/stream error occured


Defining a hook is as follows:

```js
tracker.on('HOOK_TYPE', function(value) {
	// do something with value
});
```

**Options reference**

`tracker.detectorModel` - detector instance, default: `poseDetection.SupportedModels.MoveNet`

`tracker.detectorConfig` - detector config

`tracker.autofit` bool, enable autofit/rescale points on canvas CSS auto-scaling, default: `false`

`tracker.enableAI` bool, enable or disable tracking, default: `true`

`tracker.enableVideo` bool, enable or disable draw video on cnvas, default: `true`

`tracker.enable3D` bool, enable or disable 3D keypoints, default: `false`

`tracker.pointWidth` int, width of line between points, default: `6`

`tracker.pointRadius` int, point circle radius, default: `8`

`tracker.minScore` float, minimum threshold (score) for estimated points, default: `0.35`

`tracker.log` bool, enable logging to console, default: `true`

`tracker.el3D` string, HTML element for 3D keypoint, default: `#view_3d`

`tracker.elCanvas` string, HTML element for canvas, default: `#canvas`

`tracker.elVideo` string, HTML element for video, default: `#video`


All options must be defined before calling `run()` method.


___

## Live demo: https://szczyglis.dev/js-ai-body-tracker

![demo_www](https://user-images.githubusercontent.com/61396542/180053192-4342567b-1cab-49bb-813d-b96f3a337f5e.jpg)


# Changelog
**- 1.0.0** - published first release (2022-07-20)


# Credits
 
### JS AI BODY TRACKER is free to use but if you liked then you can donate project via BTC: 

**14X6zSCbkU5wojcXZMgT9a4EnJNcieTrcr**

or by PayPal:
 **[https://www.paypal.me/szczyglinski](https://www.paypal.me/szczyglinski)**


**Enjoy!**

MIT License | 2022 Marcin 'szczyglis' Szczygliński

https://github.com/szczyglis-dev/js-ai-body-tracker

https://szczyglis.dev/js-ai-body-tracker

Contact: szczyglis@protonmail.com
