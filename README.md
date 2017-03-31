<html>
<head>
<title>webRTC Test</title>
</head>
<body onload="init();" style="background-color:#ababab;" >
<div style="width:352px; height:625px; margin:0 auto; background-color:#fff;" >
    <div>
      <video id="camFeed" width="320" height="240" autoplay>
    </video>
  </div>

    <div>
        <canvas id="photo" width="320" height="240">
        </canvas>
    </div>

    <div style="margin:0 auto; width:82px;">
        <input type="button" value="Take Photo" onclick="takePhoto();">
    </div>
</div><style>
video {
  width: 307px;
  height: 250px;
  background: rgba(255,255,255,0.5);
  border: 1px solid #ccc;
}
.grayscale {
  +filter: grayscale(1);
}
.sepia {
  +filter: sepia(1);
}
.blur {
  +filter: blur(3px);
}
/* ... */
</style>

<video autoplay></video>

<script>
var idx = 0;
var filters = ['grayscale', 'sepia', 'blur', 'brightness', 'contrast', 'hue-rotate',
               'hue-rotate2', 'hue-rotate3', 'saturate', 'invert', ''];

function changeFilter(e) {
  var el = e.target;
  el.className = '';
  var effect = filters[idx++ % filters.length]; // loop through filters.
  if (effect) {
    el.classList.add(effect);
  }
}

document.querySelector('video').addEventListener('click', changeFilter, false);
</script><script>
function init()
{
    if(navigator.webkitGetUserMedia)
    {
        navigator.webkitGetUserMedia({video:true}, onSuccess, onFail);
    }
    else
    {
        alert('webRTC not available');
    }
}

function onSuccess(stream)
{
    document.getElementById('camFeed').src = webkitURL.createObjectURL(stream);
}

function onFail()
{
    alert('could not connect stream');
}

function takePhoto()
{
    var c = document.getElementById('photo');
    var v = document.getElementById('camFeed');
    c.getContext('2d').drawImage(v, 0, 0, 320, 240);
}
</script>
</body>
</html>
