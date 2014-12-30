
# How to integrate more easily


## Step 1 : Import the SDK

SMS SDK use project depend on the way to complete the integration.Specific steps are as follows:

* 1.Copy "SMSSDK" directory to your own project in the same directory, and import it into Eclipse:
  ![img](http://wiki.mob.com/wp-content/uploads/2014/09/QQ截图20141230112627.png)
* 2.Right click your project, select "properties" in the sidebar, select "Android" in the pop-up window, and the reference projects selected "SMSSDK"
  ![img](http://wiki.mob.com/wp-content/uploads/2014/09/QQ截图20141230112820.png)

## Step 2 : Configuration AndroidManifest. XML

* Open your project "androidmanifest.xml", add the following permissions,then play under "application" to add the following activity:
```` xml
<uses-permission android:name="android.permission.READ_CONTACTS" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.RECEIVE_SMS" />
<uses-permission android:name="android.permission.GET_TASKS" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

<activity
  android:name="cn.smssdk.SMSSDKUIShell"
  android:configChanges="keyboardHidden|orientation|screenSize"
  android:theme="@android:style/Theme.Translucent.NoTitleBar"
  android:windowSoftInputMode="stateHidden|adjustResize" />
```

## Step 3 : Add code

* start SDK:
```` java
SMSSDK.initSDK(this, "<appkey>", "<appsecret>");
```
* Gui

 SMS SDK with built-in GUI function of open source, you can by calling the following code to open the message validation page:
```` java
RegisterPage registerPage = new RegisterPage();
registerPage.setRegisterCallback(new EventHandler() {
public void afterEvent(int event, int result, Object data) {

if (result == SMSSDK.RESULT_COMPLETE) {
@SuppressWarnings("unchecked")
HashMap<String,Object> phoneMap = (HashMap<String, Object>) data;
String country = (String) phoneMap.get("country");
String phone = (String) phoneMap.get("phone"); 
registerUser(country, phone);
}
}
});
registerPage.show(context);

protected void onDestroy() {
		SMSSDK.unregisterAllEventHandler();
		super.onDestroy();
	}
```

 At the same time, SMS SDK are built through the device contacts for this application in the function of the user list, can use the following code to open the "contacts friends" page:
```` java
ContactsPage contactsPage = new ContactsPage();
contactsPage.show(context);
```


 
