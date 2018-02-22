# Android-Job-XamarinBinding
Xamarin Binding for Android-Job (by Evernote)

See the project https://github.com/evernote/android-job

This binding allows you to use the library in Xamarin.Android C#

## Library
This binding project will output a dll file in the Debug or Release mode which you need to reference in your Xamarin.Android Project.

### Additional References
Using NuGet, install the following (Accept and install all extra packages when asked):
+ Xamarin.Android.Support.Compat
+ Xamarin.Android.Support.v4
+ Xamarin.GooglePlayServices.Gcm (Not required, but will work beter and support even more devices)

### Proguard
You need to include the following lines in your android project's proguard.cfg file:

    -dontwarn com.evernote.android.job.gcm.**
    -dontwarn com.evernote.android.job.GcmAvailableHelper
    
    -keep public class com.evernote.android.job.v21.PlatformJobService
    -keep public class com.evernote.android.job.v14.PlatformAlarmService
    -keep public class com.evernote.android.job.v14.PlatformAlarmReceiver
    -keep public class com.evernote.android.job.JobBootReceiver
    -keep public class com.evernote.android.job.JobRescheduleService

### Android Manifest
You need to add the following in your Android Manifest under application for the services and receivers to work properly.

    <service android:name="com.evernote.android.job.v21.PlatformJobService" android:exported="false" android:permission="android.permission.BIND_JOB_SERVICE"/>
    <service android:name="com.evernote.android.job.v14.PlatformAlarmService" android:exported="false" android:permission="android.permission.BIND_JOB_SERVICE"/>
    <service android:name="com.evernote.android.job.v14.PlatformAlarmServiceExact" android:exported="false"/>
    <receiver android:name="com.evernote.android.job.v14.PlatformAlarmReceiver" android:exported="false">
      <intent-filter>
        <!-- Keep the filter for legacy intents -->
        <action android:name="com.evernote.android.job.v14.RUN_JOB"/>
        <action android:name="net.vrallev.android.job.v14.RUN_JOB"/>
      </intent-filter>
    </receiver>
    <receiver android:name="com.evernote.android.job.JobBootReceiver" android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="android.intent.action.QUICKBOOT_POWERON"/>
        <action android:name="com.htc.intent.action.QUICKBOOT_POWERON"/>
        <action android:name="android.intent.action.MY_PACKAGE_REPLACED"/>
      </intent-filter>
    </receiver>
    <service android:name="com.evernote.android.job.gcm.PlatformGcmService" android:enabled="false" android:exported="true" android:permission="com.google.android.gms.permission.BIND_NETWORK_TASK_SERVICE">
      <intent-filter>
        <action android:name="com.google.android.gms.gcm.ACTION_TASK_READY"/>
      </intent-filter>
    </service>
    <service android:name="com.evernote.android.job.JobRescheduleService" android:exported="false" android:permission="android.permission.BIND_JOB_SERVICE"/>
	
Also make sure to have the following permissions:

    <uses-permission android:name="android.permission.WAKE_LOCK"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>

### Usage
The same as the original project <a href="https://github.com/evernote/android-job#usage" target="_blank">here</a>