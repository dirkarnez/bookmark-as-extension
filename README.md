bookmark-as-extension
=====================
[dirkarnez/bookmarklet-generator](https://github.com/dirkarnez/bookmarklet-generator)
### Bookmark
```javascript
javascript:navigator.clipboard.writeText(`[${document.title}](${window.location.href})`).then(a => alert("done"));
```

### Avoid close tab
```
javascript:window.onbeforeunload = ()  => { return "You have attempted to leave this page. Are you sure?"; }
```

### Audio volumne (from [dirkarnez/web-audio-gain-example](https://github.com/dirkarnez/web-audio-gain-example))
```
javascript:((gainValue) => { const video = document.querySelector('video'); if (!window.myGainNode) { const myAudioContext = new AudioContext(); const sourceNode = myAudioContext.createMediaElementSource(video); window.myGainNode = myAudioContext.createGain(); sourceNode.connect(window.myGainNode); window.myGainNode.connect(myAudioContext.destination); } window.myGainNode.gain.value = gainValue; })(prompt("Default is 1, enter the gain"))
```
