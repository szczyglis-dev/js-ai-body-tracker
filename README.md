Release: **1.0.1** | build: **2024.08.26** | Javascript / TensorFlow JS

# JS AI BODY TRACKER - tracker.js

**JS AI Body Tracker `(tracker.js)` is a JavaScript library that implements machine learning-based models for human pose estimation and movement analysis. The library is written in JavaScript and does not require Node.js. It supports three different models for detecting human poses in videos: `MoveNet`, `PoseNet`, and `BlazePose`. The library offers real-time video analysis from three different sources: web/smartphone cameras, video files (mp4, mkv, avi, webm), and online streaming (IPTV/m3u8).**
## Features

- Easy to implement in your own JavaScript application
- Works in real-time directly in the browser
- Supports multiple video sources: web cameras, video files (mp4, mkv, avi, webm), online streams (IPTV/m3u8)
- Offers three different neural network models: `MoveNet`, `PoseNet`, and `BlazePose`
- Provides real-time 3D mapping (BlazePose)
- Can be easily extended with events and hooks
- Consists of only one file for direct import into your application; no Node.js required
- Uses `TensorFlow JS`, `ScatterGL`, and `videoJS` libraries

Real-time Human Pose Estimation on MP4 Video:

![gif1](https://user-images.githubusercontent.com/61396542/180048048-ebd4fdbe-9b0e-43a8-b34a-255bd092e366.gif)
![gif2](https://user-images.githubusercontent.com/61396542/180047990-523f6706-1241-4cd6-9114-8e1e887cce7f.gif)

Real-time human pose estimation on IPTV/m3u8 online stream:

![gif3](https://user-images.githubusercontent.com/61396542/180048146-80cf69b3-26ac-4841-bbe5-7c16cc757491.gif)


## Live demo

A demo of a real-time working sample application using the library can be found here:

## https://szczyglis.dev/js-ai-body-tracker


There are three input video sources available in the demo application: web camera, video file, and IPTV/m3u8 stream. The entire process of image analysis takes place in real-time.

## Basic usage

```js
// javascript

tracker.setModel('MoveNetSinglePoseLightning'); // define model to use

tracker.elCanvas = '#canvas'; // define HTML canvas container
tracker.elVideo = '#video'; // define HTML video container
tracker.el3D = '#view_3d'; // define HTML container for 3D view 

tracker.run('camera'); // run
```
The repository includes a sample application that illustrates the operation and use of the library.

## Usage step by step

First, you need to define two HTML elements: a video and a canvas:

```html
<canvas id="canvas" width="500" height="500"></canvas>
<video id="video" width="500" height="500">
	<source src="">
</video>
```
Next, you need to import the library and configure it:

```html
<script src="./js/tracker.js"></script>
<script>
	tracker.setModel('MoveNetSinglePoseLightning');	
	tracker.elCanvas = '#canvas';
	tracker.elVideo = '#video';
	tracker.run('camera');
</script>
```

### Examples of use

**1) VIDEO INPUT: Webcam / Smartphone Camera**

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
The above code activates the camera, initializes the model for detecting human poses, and then displays the detected points on the video from the camera on the canvas element in real time, superimposing them on the input from the webcam.

**2) VIDEO INPUT: Movie File (mp4, mkv, avi, webm)**

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
The above code loads the movie `movie.mp4`, initializes the human pose analysis model, and then displays the detected points on the video in real time on the canvas, superimposing them on the input video.

**3) VIDEO INPUT: Online Stream (IPTV/m3u8)**

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
The above code opens an `.m3u8` online video stream, initializes the human pose detection model, and then displays the detected points on the video stream superimposed on the stream image in the canvas element in real-time. **Note that the `videoJS` library is used to handle the stream.**

### Configuration

**Model**

The library has preconfigured settings for three different neural network models. You can use these settings or define all options manually. To use the predefined model, use the `setModel()` method:
```js
tracker.setModel('MoveNetSinglePoseLightning');
```

**Available models**

- `MoveNetSinglePoseLightning`			
- `MoveNetSinglePoseThunder`
- `MoveNetMultiPoseLightning`
- `PoseNetMobileNetV1`
- `PoseNetResNet50`
- `BlazePoseLite`
- `BlazePoseHeavy`
- `BlazePoseFull`

You can also define the settings manually, for example, using the MoveNet network with the MULTIPOSE settings:
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
The models differ in efficiency and accuracy. You can read more about these neural network models on the Google website:
https://github.com/tensorflow/tfjs-models/tree/master/pose-detection


**Input video source**

You can define three different video sources:

- `camera`
- `video`
- `stream`

To select a source, call the method `run()` with the source name passed as an argument, e.g.:
```js
tracker.run('camera') // takes video from the webcam
```
```js
tracker.run('video') // takes video from a movie file (e.g., mp4)
```
```js
tracker.run('stream') // takes video from an m3u8 online stream
```

**DOM Elements Configuration**

You need to define elements for video, canvas, and for 3D output (only available for the BlazePose model). To do this, set the appropriate values:
```js
tracker.elCanvas = '#canvas';
tracker.elVideo = '#video';
tracker.el3D = '#view_3d';
```

**Display Settings**

You can define the size of points drawn on the canvas:

```js
tracker.pointWidth = 6; // point connection width
tracker.pointRadius = 8; // point circle radius
```

**Events / Hooks**

You can define your own functions to handle specific tasks, such as processing points in the image detected by the neural network. The event/hook system is used for this purpose. To define a hook, use the `on()` method. For example, to define a hook that displays all detected points in real-time, write the following code:
```js
tracker.on('beforeupdate', function(poses) {
	console.log(poses);
});
````

The above code will make the console display a set of points detected in the image when rendering each frame.

You can define hooks for five types of events:

- `beforeupdate` - Executes before the canvas is rendered in every frame
- `afterupdate` - Executes after the canvas is rendered in every frame
- `statuschange` - Executes when the status changes
- `detectorerror` - Executes when a detector error occurs
- `videoerror` - Executes when a video/stream error occurs

Defining a hook is done as follows:

```js
tracker.on('HOOK_TYPE', function(value) {
	// do something with value
});
```
**3D Pose Estimation**

To display the detected points in 3D space, enable the `enable3D` option, as shown below:
```js
tracker.enable3D = true;
```
An HTML element (e.g., a div) must also be created to act as a container for the 3D output. Define the element as shown below:
```html
<body>
	...
	<div id="view_3d"></div>

	<script>
		tracker.el3D = '#view_3d';
		tracker.enable3D = true;
```

3D keypoints are displayed using the `ScatterGL` library.

![3dok](https://user-images.githubusercontent.com/61396542/180082333-e7793d65-5214-4354-bf61-97c3494a08ec.gif)

**Options reference**

`tracker.detectorModel` - detector instance, default: `poseDetection.SupportedModels.MoveNet`

`tracker.detectorConfig` - detector config

`tracker.autofit` bool, enable autofit/rescale points on canvas CSS auto-scaling, default: `false`

`tracker.enableAI` bool, enable or disable tracking, default: `true`

`tracker.enableVideo` bool, enable or disable display original video on canvas, default: `true`

`tracker.enable3D` bool, enable or disable 3D keypoints, default: `false`

`tracker.pointWidth` int, width of line between points, default: `6`

`tracker.pointRadius` int, point circle radius, default: `8`

`tracker.minScore` float, minimum threshold (score) for estimated points, default: `0.35`

`tracker.log` bool, enable logging to console, default: `true`

`tracker.el3D` string, HTML element for 3D keypoint, default: `#view_3d`

`tracker.elCanvas` string, HTML element for canvas, default: `#canvas`

`tracker.elVideo` string, HTML element for video, default: `#video`



The following options should be defined before calling the `run()` method: `detectorModel`, `detectorConfig`, `elCanvas`, `elVideo`, `el3D`.


___

## Live demo: https://szczyglis.dev/js-ai-body-tracker

![demo_www](https://user-images.githubusercontent.com/61396542/180053192-4342567b-1cab-49bb-813d-b96f3a337f5e.jpg)


## Changelog

**1.0.0** -- First release published (2022-07-20)

**1.0.1** -- Improved documentation (2024-08-26)


--- 
**JS AI Body Tracker is free to use, but if you like it, you can support my work by buying me a coffee ;)**

https://www.buymeacoffee.com/szczyglis

**Enjoy!**

MIT License | 2022 Marcin 'szczyglis' Szczygliński

https://github.com/szczyglis-dev/js-ai-body-tracker

https://szczyglis.dev/js-ai-body-tracker

Contact: szczyglis@protonmail.com

