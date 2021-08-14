# Basic-Camera-
This will be the Basic Camera using HTML.

Source code:
<html>
<head>
<title>Simple Camera</title>
<link rel="stylesheet" href="Approved htmls/Offline IDE/font-awesome/css/font-awesome.min.css">
<meta name="viewport" content="user-scalable=no,initial-scale=1,maximum-scale=1">
<style type="text/css">
video {
width: 100%;
}
i {
font-size: 20px;
}
</style>
</head>
<script type="text/javascript">
var options = {
video:null,
audio:null
}
//start video
function start_video() {
navigator.mediaDevices.getUserMedia(options).then(function(stream){
document.getElementById("camera_view").srcObject = stream;
}).catch((error) => {
document.getElementById("errors").innerHTML = error;
});
}
function to_boolean(bol) {
if (bol == "true") {
return true;
}
else if (bol == "false") {
return false;
} else {
return bol;
}
}
function load_data() {
var mic = localStorage.getItem("mic");
var vid = localStorage.getItem("vid");
//check if mic has already been configured
if (mic != null) {
options.audio = to_boolean(mic);
document.getElementById("mic_enable").checked = to_boolean(mic);
} else {
document.getElementById("mic_enable").checked = true;
options.audio = true;
}
//check if video has already been configured
if (vid != null) {
options.video = to_boolean(vid);
document.getElementById("vid_enable1").checked = to_boolean(vid);
} else {
document.getElementById("vid_enable1").checked = true;
options.video = true;
}
start_video();
}
//configure mic
function mic(enable) {
localStorage.setItem("mic",enable);
load_data();
}
//configure vid
function vid(enable) {
localStorage.setItem("vid",enable);
load_data();
}
</script>
<body onLoad="load_data();">
<video id="camera_view" autoplay></video>
<hr>
<i class="fa fa-microphone"> Mic <input type="checkbox" id="mic_enable" onClick="mic(this.checked);"></i>
<br>
<br>
<i class="fa fa-camera"> Video <input type="checkbox" id="vid_enable1" onClick="vid(this.checked);"></i>
<hr>
<div id="errors">
</div>
</body>
</html>
