# AddCall
Make audio and video calls with WebRTC with just 3 lines of code.

We will divede de instalation in two parts. Server and Android

## Server Instalation

#### Requirement
- Hosting with Root access and able to be installed NodeJS

#### Instalation steps

1. Unzip the downloaded files and copy and paste "addcall server.zip" to your hosting and unzip it.
2. in your command or terminal type:

```
$ cd /HOME/ADDCAL_DIRECTORY
```
Then Start the AddCall Server by running of of there commands

```
$ npm start index.js
```
or you also can use

```
$ node index.js
```

Your terminal or command line interface will print or log `AddCall Server is on port 8880` 

3. Then go to your browser and enter the url and port ex: `http://yourdomain.com:8880/` you must get message `AddCall Server is running!` 

4. If you want to change the port, just open file `index.js` and search for `app.set('port', process.env.PORT || 8880);` and chnage the port `8880` to what you want. 

5. Thats all. remeber that you also can use our Server URL but, it may be offline or slow somtimes because we still working to update it.

## Android Side Instalation

#### Requirement
- Android Studio or Other IDE the support Gradle
- Existing Android App project or Create new Android App project

#### Instalation steps



```java
dependencies {
    implementation project(':addcall')
}
```

## HOW TO USE THE LIBRARY

### Setup and initialization

**Step 1:** Setup AddCall and Initialize using your server configuration and purchase code you get from envato:

```java
import com.angopapo.addcall.AddCall;
import android.app.Application;

public class App extends Application {
  @Override
  public void onCreate() {
    super.onCreate();
    
    // Initilize AddCall Server
    AddCall.connect(new AddCall.Config.Builder(this).server("ServerURL").clientKey("PurchaseCode").build());
    
  }
}
```
The custom **Application** class must be registered in `AndroidManifest.xml`:

```java
<application
   android:name=".App"
   ...>
   ...
 </application>
```

**Step 2:** Anywhere in your app or in your mainActivity you need to register the users details

```java
AddCall.start(new AddCall.Config.SessionManager(this)
                .currentUserId("12jhdbs")
                .currentUserFullName("John Doe")
                .currentUserPhotoUrl("http://www.image.com/photo.jpg")
                .build());
```

**Step 3:** In your adapter or anywhere you want to call user. 

```java

AddCall.CallBuilder(new AddCall.Config.CallsManager(mActivity)
                    .receiverUserId("Hde73dds")
                    .isVideoCall(true) // True for Video Call and False for Voice Call
                    .receiverUserPhotoUrl(http://www.image.com/photo.jpg)
                    .receiverUserFullName("Jonh Doe 2")
                    .build());

```

### Get Extras information you may need.
For better performance use in **Application class**

**Call detials:** You may want to get call info after the call hangup or finish. 

```java

        HostCall hostCall = new HostCall();
        addCall.setCallHistoryResultListener(new AddCall.CallHistoryResultListener() {
            @Override
            public void onCallFinished(boolean isAcceptedCall, boolean isVideoCall, String duration, String callerId, String receiverId) {

                AddCallHelper.LogCat("Call finished: " + " isAcceptedCall: " + isAcceptedCall + " isVideoCall: " + isVideoCall + " duration: " + duration + " called by UserId : " + callerId + " receiver by UserId: " + receiverId, AddCallHelper.success);
            }
        });
        
```

**CallerID:** AddCall uses Sockei.io and for any reason if you want to get Users CallerId.

```java
        AddCall addCall = new AddCall();
        addCall.setCallerIdListener(new AddCall.CallerIdListener() {
            @Override
            public void onCallerIdChanged(String callerId) {
            
                // Use it for your purposes.
                hostCallHelper.LogCat("New callerId is: " + callerId, hostCallHelper.success);
            }
        });
```

### Author
Thanks for buying our code
For help and any informations please conatct us via:

**Email:** maravilhosinga@gmail.com
**WhatsApp:** +33614778601
