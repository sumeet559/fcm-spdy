# fcm-spdy
FCM using HTTP/2 client

Documentation and use of APIs is exactly same as https://www.npmjs.com/package/fcm-node.
The package uses HTTP/2 client for posting payload.

# Sample Code
```js
  'use strict'
  var koa = require('koa');
  var app = koa();

  var FCM = require('fcm-spdy');

  var fcm = new FCM(API_KEY);//same that was used in gcm

  app.use(function *(){

    var message = { //this may vary according to the message type (single recipient, multicast, topic, et cetera)
    to: 'notification id or device token',
    collapse_key: 'your_collapse_key',

    notification: {
    title: 'Title of your push notification',
    body: 'Body of your push notification'
    },

    data: { //you can send only notification or only data(or include both)
    my_key: 'my value',
    my_another_key: 'my another value'
    }
    };

    fcm.send(message, function(err, response){
    if (err) {
    console.log("Something has gone wrong!",err);
    } else {
    console.log("Successfully sent with response: ", response);
    }
    });

  }
  );
app.listen(8000);
```
Now just open localhost:8080 in the browser
