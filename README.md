<html>
  <head>
    <title>My First Music Player</title>
    <link rel="shortcut icon" href="http://www.bilibili.com/favicon.ico">
  </head>
  <body>
    <div>
      <ul class="List">
        <li>Set Your Url</li>
        <li><input value="Set Your Url" id="SetUrl" onkeydown="JavaScript:if (event.keyCode==13) {setTimeout(function(){MusicSetSrc(document.getElementById('SetUrl').value)},1);}"></li>
        <li><button onclick="MusicSetSrc(document.getElementById('SetUrl').value)">Update</button></li>
      </ul>
      <br>
      <ul class="List">
        <li><button onclick="MusicPlay()">Play/Pause</button></li>
        <li><button onclick="MusicStop()">Stop</button></li>
        <li><button onclick="Update__()">Show / hide controls</button></li>
      </ul>
    </div>
    <br>
    <div>
      <ul>
        <li>Music Url:<span id="getUrl">undefined</span></li>
        <li>Music Long:<span id="getLong">undefined</span></li>
        <li>Music Played Time:<span id="getPlayedTime">undefined</span></li>
        <li>Music Played Time:<span id="getTime">undefined</span></li>
        <li>Music Is Playing:<span id="getIsPlaying">undefined</span></li>
        <li>Mode By GYHHY</li>
      </ul>
    </div>
    <audio style="width : 100%"></audio>
    <script>
    var musicPlayer = document.getElementsByTagName('audio')[0];
    var isSee = true;
    musicPlayer.controls = true;
    musicPlayer.paused = true;
    function MusicPlay(){
      if (musicPlayer.paused) {
        musicPlayer.play();
      } else {
        musicPlayer.pause();
      }
    }
    function MusicStop() {
      musicPlayer.pause();
      musicPlayer.currentTime = 0;
    }
    function MusicSetSrc(Url) {
      if (Url) {
        if (musicPlayer.src != Url) {
          musicPlayer.src = Url;
        }
        return true;
      }
      return false;
    }
    function Update__() {
      var TempFun = function(i_,Time) {
        setTimeout(function() {
          musicPlayer.style=("width : "+i_+"%")
        }, Time);
      }
      if (!isSee) {
        musicPlayer.controls = true;
        for (var i=0;i<=100;i++){
          TempFun(i,i*10);
        }
      } else {
        for (var i=100;i>=0;i--) {
          TempFun(i,(100-i)*10);
        }
        setTimeout(function () {
          musicPlayer.controls = false;
        }, 1000);
      }
      isSee = (!isSee);
    }
    var Update_ = function(){
      document.getElementById('getUrl').innerHTML = musicPlayer.src;
      document.getElementById('getLong').innerHTML = Math.round(musicPlayer.duration*10)/10;
      document.getElementById('getPlayedTime').innerHTML = Math.round(musicPlayer.currentTime*10)/10;
      var PlayedTime = 0;
      try {
        PlayedTime = Math.round(Math.round((musicPlayer.currentTime/musicPlayer.duration)*1000))/10;
      } catch (e) {
      } finally {
        if (isNaN(PlayedTime)){
          PlayedTime = 0;
        }
        document.getElementById('getTime').innerHTML = String(PlayedTime)+"%";
      }
      document.getElementById('getIsPlaying').innerHTML = (!musicPlayer.paused)
    }
    setInterval(Update_, 100);
    </script>
    <style>
    li {
      list-style : none;
    }
    ul.List li {
      float: left;
    }
    </style>
  </body>
</html>
