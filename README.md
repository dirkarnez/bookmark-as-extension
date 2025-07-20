bookmark-as-extension
=====================
[dirkarnez/bookmarklet-generator](https://github.com/dirkarnez/bookmarklet-generator)
### Bookmark
```javascript
javascript:navigator.clipboard.writeText(`[${document.title}](${window.location.href})`).then(a => alert("done"));
```

### Loop video
```javascript
javascript:(() => {  document.getElementsByTagName("video")[0].loop = true; })();
```

### Avoid close tab
```javascript
javascript:window.onbeforeunload = ()  => { return "You have attempted to leave this page. Are you sure?"; }
```

### Disable Page Visibility API
```javascript
javascript:(() => {for (event_name of ["visibilitychange", "webkitvisibilitychange", "blur"]) { window.addEventListener(event_name, function(event) { event.stopImmediatePropagation(); }, true); }})()
```

### IG loop video
```javascript
javascript:(() => { for (event_name of ["visibilitychange", "webkitvisibilitychange", "blur"]) { window.addEventListener(event_name, function(event) { event.stopImmediatePropagation(); }, true); for (var i = 0; i < document.getElementsByTagName("video")[0].parentNode.childNodes.length; i++) { if (document.getElementsByTagName("video")[0].parentNode.childNodes[i] != document.getElementsByTagName("video")[0]) { document.getElementsByTagName("video")[0].parentNode.removeChild(document.getElementsByTagName("video")[0].parentNode.childNodes[i]); } }; document.getElementsByTagName("video")[0].controls = true; }})()
```

### Audio volumne (from [dirkarnez/web-audio-gain-example](https://github.com/dirkarnez/web-audio-gain-example))
```javascript
javascript:((gainValue) => { const video = document.querySelector('video'); if (!window.myGainNode) { const myAudioContext = new AudioContext(); const sourceNode = myAudioContext.createMediaElementSource(video); window.myGainNode = myAudioContext.createGain(); sourceNode.connect(window.myGainNode); window.myGainNode.connect(myAudioContext.destination); } window.myGainNode.gain.value = gainValue; })(prompt("Default is 1, enter the gain"))
```

### Apache Guacamole keep session ([UDS](https://puuds.polyu.edu.hk/uds/page/services))
```javascript
function makeid(length) {
    var result           = '';
    var characters       = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
    var charactersLength = characters.length;
    for ( var i = 0; i < length; i++ ) {
        result += characters.charAt(Math.floor(Math.random() * charactersLength));
    }
    return result;
}

function dostuff() {
    new Promise(res => {
        const string = makeid(1);
        setTimeout(() => {
            const event = new KeyboardEvent('keydown', {
                key: string,
                code: `Key${string.toUpperCase()}`,
                char: string,
                keyCode: string.charCodeAt(0),
                bubbles: true,
            });
            document.activeElement.dispatchEvent(event);
            
            // Dispatch input event to update the value
            document.activeElement.value += string;
            document.activeElement.dispatchEvent(new Event('input', { bubbles: true }));
            res();
        }, 1000);
    })
    .then(() => {
        dostuff();
    });
}

dostuff();
```
