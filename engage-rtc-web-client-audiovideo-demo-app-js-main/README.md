# engage-rtc-web-client-audiovideo-demo-app-js
Engage RTC click to call web application describs how you can easily integrate click-to-call feature into your website. The javascript files provided here will abstract away the logic of connecting to the Engage Digital platform, making the calls, binding local and remote videos to the html etc.
It can be easily plugged into an existing website with minimal changes.

#### Follow this guide step by step, to integrate Engage Platform's click-to-call feature to your Website.

Copy the below files to the root of your web application. For evaluation purpose you can create a folder `eg: myApp` and copy the files there.
- engage-digital-click-to-call-config.js
- engage-digital-click-to-call.js

Update your web page by incorporating the below UI elements. For evaluation purpose you can create an `index.html` in myApp folder and place the below contents there.

Create a button, so that user can click on this button to make a call\
Example:
```html
<button id="engage-digital-click-to-call-btn">Call</button>
```
Create a video element to display the local video. Make sure autoplay, loop, muted and playsinline properties are given.\
Example:
```html
<video id="engage-digital-local-video" autoplay loop muted playsinline style="width: 300px;height: 225px;background-color: gray"></video>
```
Create a video element to display the remote video. Make sure autoplay, loop and playsinline properties are given.\
Example:
<video id="engage-digital-remote-video" autoplay loop playsinline style="width:300px;height:225px;background-color:gray"></video> 
 
Optionally you can define a div element to display important events as part of call handling. This may help in debugging.\
Example:
```html
<div id='engage-digital-alert'></div>
```
The styling and placing of these elements are entirely up to you and can be designed in a way that suites the design of your site.
So these elements can be placed anywhere and can be styled at your wish.

As an example refer the HTML content [`app-index.html`](https://github.com/RSYS-EDP/engage-rtc-click-to-call-web-app/blob/main/app-index.html) of this Demo application to see how these elements are placed in this page.

>*Note: The Ids used in these elements should be configured properly in [engage-digital-click-to-call-config.js](https://github.com/RSYS-EDP/engage-rtc-click-to-call-web-app/blob/main/engage-digital-click-to-call-config.js).
Refer Update Configuration section for more details.*

### Update Configuration
Update the configuration in `engage-digital-click-to-call-config.js` with proper values. It has the following properties.

- **engageDomain:** Engage Digital RTC domain name. Get this domain name from Engage Platform Admin. In this demo you can use the publicly hosted **rtc.engagedigital.ai**
- **callTo:** The number to dial to. It should be a proper service number. Creating the service and assigning it to a number can be done through ESMP-UI
In this demo, you can use the number 9070707120 which is available in publicly hosted ESMP portal (https://portal.engagedigital.ai)\
Note: When you dial to this number a video announcement will be played.
- **callType:** Type of call. Valid values are video or audio.
- **callBtnId:** Id of the Call Button. Make sure the same id is used in your html call button. In this example it is `engage-digital-click-to-call-btn`.
- **localVideoId:** Id of the Local Video element. Make sure the same id is used in your html local video element. In this example it is `engage-digital-local-video`.
- **remoteVideoId:** Id of the Remote Video element. Make sure the same id is used in your html remote video element. In this example it is `engage-digital-remote-video`.
- **makeCallText:** The text to be displayed in the call button.
- **disconnectCallText:** The text to be displayed on call button once the call is established or in the process of connecting. So the user will get the context and can disconnect the call.
- **alertDivId:** If this div id is given, important events will be displayed here. This can be helpful while debugging the application. In this example it is `engage-digital-alert`
- **consoleLog:** If its true, click-to-call logs as well as EngageDigital logs will be written to browser console
- **joinWithVideoMuted:** Join the call with local video muted or not. When it's true caller will join the call with local video muted.\

Add the Engage Digital click-to-call javascript files to your website just before closing the `<body>` tag as shown below. Please make sure `engage-digital-click-to-call-config.js` is included before `engage-digital-click-to-call.js`, the order of including these files is important.

```html
     <body>
        <script src="engage-digital-click-to-call-config.js"></script>
        <script src="engage-digital-click-to-call.js"></script>
     </body>
```
Congratulations, now all the changes are done. You can open the Application in browser and make a call.

>*Note With the above steps, when engage-digital-click-to-call.js is loaded, it will connect to the Engage Digital platform with the engageDomain provided in the `engage-digital-click-to-call-config.js` file.*

If you want to programmatically connect to the Engage Platform without providing this configuration file, you can call `initializeEngageDigitalClickToCall(config)` function explicitly. In that case, engage-digital-click-to-call-config.js file should not be included in your website.

Example:
```html
<body>
<!--Click to call UI elements and other content of your site -->
<script src="engage-digital-click-to-call.js"></script>
<script type="text/javascript">
initializeEngageDigitalClickToCall({
engageDomain: 'rtc.engagedigital.ai',
callTo: '9070707120',
callType: 'video',
callBtnId: 'engage-digital-click-to-call-btn',
makeCallText: 'Call',
disconnectCallText: 'End Call',
localVideoId: 'engage-digital-local-video',
remoteVideoId: 'engage-digital-remote-video',
alertDivId: 'engage-digital-alert',
consoleLog: false,
joinWithVideoMuted: false
});
</script>
</body>
```
