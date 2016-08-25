# react-native-ios-audio

react-native interface for ios avplayer

# installation
1. Run 'npm install --save react-native-ios-audio'
2. Add RNAudioPlayer.h, RNAudioPlayer.m files to "your_project" folder in XCode
   (they can also be found in node_modules/react-native-ios-audio/react-native-ios-audio)

# usage
```
var player = require('react-native').NativeModules.RNAudioPlayer;

// initialize 
player.initWithURL("http://your_audio_url");

// get duration
player.getDuration((result) => {
  var duration = result - (result % 1)
  var minutes = parseInt((duration / 60));
  var seconds = parseInt(duration % 60);
  minutes = (minutes < 10) ? "0" + minutes : minutes;
  seconds = (seconds < 10) ? "0" + seconds : seconds;
  this.setState({ duration: minutes + ":" + seconds })
})
    
// get current time (every 0.2 seconds)  
var playSubs = NativeAppEventEmitter.addListener('playListener', 
  (result) => {
    var currentTime = result.currentTime - (result.currentTime % 1)
    var minutes = parseInt((currentTime / 60));
    var seconds = parseInt(currentTime % 60);
    minutes = (minutes < 10) ? "0" + minutes : minutes;
    seconds = (seconds < 10) ? "0" + seconds : seconds;
    this.setState({ currentTime: minutes + ":" + seconds })
  }
)

// get notification when play is finished
var finishSubs = NativeAppEventEmitter.addListener('finishListener',
  (result) => {
    this.setState({ finished: "Finished now" })
  }
)

// play
player.play()

// pause
player.pause()
```
