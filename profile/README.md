## PlaceRickRollQRCode

### ToDos

- [ ] Python server
- [X] Pixelcanvas scraper
- [ ] Pixel importance based on changes --> dynamic heat maps
- [ ] connect scraper with existing commander
- [ ] Node server api
- [ ] Js userscript

### Current Endpoints (Beta):

#### [Pixel data](https://pixelcanvas-scraper.shadowlp174.repl.co/api/pixel/-497.2800)

- URL: `https://pixelcanvas-scraper.shadowlp174.repl.co/api/pixel/%x.%y`
- Return format: `JSON` or `false`
- Usage: replace `%x.%y` with actual coords. Example: [api/pixel/-497.2800](https://pixelcanvas-scraper.shadowlp174.repl.co/api/pixel/-497.2800)

This endpoint will retrieve the known data about the specified pixel (%x.%y). It will return `false` if the coordinates are not in the area of the qr code.

#### Pixel Updates

- URL: `wss://pixelcanvas-scraper.shadowlp174.repl.co/api/live`
- Return format: `JSON` on update
- Usage: connect through a websocket client to the given wss url. Then listen for the onmessage event.

This enpoint will fire pixel updates to the connected clients, if the occured update was inside our area.

Example code:

```JavaScript
const socket = new WebSocket('wss://pixelcanvas-scraper.shadowlp174.repl.co/api/live');
socket.onopen = () => {
  console.log("Connected to server");
};
  
socket.onmessage = (msg) => {
  var data;
  try {
    data = JSON.parse(msg.data);
  } catch (e) {
    console.log("Invalid JSON: ", e, msg);
    return;
  }

  switch (data.type.toLowerCase()) {
    case "update":
      console.log("Pixel update received: ", data.data);
      var p = document.createElement("p");
      p.innerHTML = "Pixel update: " + JSON.stringify(data.data);
      document.getElementById("logs").appendChild(p);
    break;
    default:
      console.log("Data received: ", data);
      var p = document.createElement("p");
      p.innerHTML = "Data: " + JSON.stringify(data.data);
      document.getElementById("logs").appendChild(p);
    break;
  }
};
```

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
