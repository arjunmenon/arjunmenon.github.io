---
layout: post
title:  "Sending a basic Upnp request!"
date:   2017-12-31 21:54:38 +0530
categories: openhome upnp
---
Through curl 
```bash
url = "http://192.168.1.4:49152/ctl/OHInfo"
header = "Content-Type: text/xml; charset=utf-8"
header = "SOAPAction: \"urn:av-openhome-org:service:Info:1#Details\""
data = "<?xml version=\"1.0\" encoding=\"utf-8\"?><s:Envelope s:encodingStyle=\"http://schemas.xmlsoap.org/soap/encoding/\" xmlns:s=\"http://schemas.xmlsoap.org/soap/envelope/\"><s:Body><u:Details xmlns:u=\"urn:av-openhome-org:service:Info:1\"></u:Details></s:Body></s:Envelope>"
```
This request will return the device details of the Openhome renderer.  

Take note of the single/double quotes in the header and data. They are mandated by the Upnp spec sheet

Through Javascript 
```javascript
var req = new tabris.XMLHttpRequest();
req.open('POST', 'http://192.168.1.6:49152/ctl/RenderingControl', true);
req.setRequestHeader('Content-Type', 'text/xml; charset="utf-8"');
req.setRequestHeader('SOAPAction', '"urn:schemas-upnp-org:service:RenderingControl:1#GetVolume"');
req.onreadystatechange = function () {
 if (req.readyState === req.DONE) {
  console.log(req.response);
 }
};

var payload = `<?xml version="1.0"?>
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/" s:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">
 <s:Body>
  <u:GetVolume xmlns:u="urn:schemas-upnp-org:service:RenderingControl:1">
   <InstanceID>0</InstanceID>
   <Channel>Master</Channel>
  </u:GetVolume>
 </s:Body>
</s:Envelope>`;

req.send(payload);
```
This request would return the current master volume of the Upnp renderer.  

Not all Openhome and Upnp services are interchangeable.  

Communicating with Openhome/Upnp services is an exact science.   
Requests has to be formatted **exactly** as expected in the docs. All quotes, content-type, xml data etc need to be cared for.