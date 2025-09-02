bookmark-as-extension
=====================
[dirkarnez/bookmarklet-generator](https://github.com/dirkarnez/bookmarklet-generator)
### Bookmark as markdown
```javascript
javascript:navigator.clipboard.writeText(`[${document.title}](${window.location.href})`).then(a => alert("done"));
```

### Bookmark as HTML
```javascript
javascript:navigator.clipboard.writeText(`<a href="${window.location.href}" target="_blank">${document.title}</a>`).then(a => alert("done"));
```

### Delete Workflow action
```javascript
javascript:document.querySelector("* > div.Overlay-footer.Overlay-footer--alignEnd.d-block > form > button").click()
```

### eBook
```javascript
javascript:(() => { const downloadFile = (imgUri, name) => { const link = document.createElement('a'); document.body.appendChild(link); link.href = imgUri; link.target = '_self'; link.download = name; link.click() }; const serial = funcs => funcs.reduce((promise, func) => promise.then(result => func().then(Array.prototype.concat.bind(result))), Promise.resolve([])); serial(Array(window.bookData.pageCount).fill(NaN).map((_, i) => () => new Promise(res => setTimeout(() => { bookData.getPageManifest(i, true, data => { downloadFile(data.url, `${`${i}`.padStart(`${window.bookData.pageCount - 1}`.length, "0")}.jpg`); res(); }); }, 1000)))); })();
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

### YouTube playlist all unique
```javascript
javascript:(() => {const names = Array.from(document.getElementsByClassName("yt-simple-endpoint style-scope ytd-playlist-video-renderer")).map(a => a.innerText);alert([...new Set(names)].length == names.length && names.every(a => a != `[Deleted video]`) ? `${[...new Set(names)].length} unique videos found` : `false`);})();
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

function dostuff({ signal }) {
    new Promise((resolve, reject) => {
        if (signal.aborted) {
            reject(signal.reason);
            return;
        }
        const string = makeid(1);
        const handle = setTimeout(() => {
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
            resolve();
        }, 1000);
        signal.addEventListener("abort", () => {
            // Stop the main operation
            // Reject the promise with the abort reason.
            clearTimeout(handle);
            reject(signal.reason);
        });
    })
    .then(() => {
        dostuff({ signal });
    });
}

const controller = new AbortController();
dostuff({ signal: controller.signal });
// to stop:
// controller.abort(); 
```
