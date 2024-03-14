bookmark-as-extension
=====================
### Bookmark
```javascript
javascript:navigator.clipboard.writeText(`[${document.title}](${window.location.href})`).then(a => alert("done"));
```

### Avoid close tab
```
javascript:window.onbeforeunload = ()  => { return "You have attempted to leave this page. Are you sure?"; }
```
