---
title: adb 获取 Android 基本信息
date: 2020-04-09 11:17:30
tags: ['Android', 'Adb']
categories: [Android]
---

### android_id
#### 什么是 android_id

#### 获取 android_id
代码获取

```java
public static String getAndroidId(Context context) {
    return Settings.System.getString(contentResolver, Settings.System.ANDROID_ID);
}

public static String getAndroidId(Context context) {
    return Settings.Secure.getString(contentResolver, Settings.Secure.ANDROID_ID);
}

```

adb 获取

```shell
# adb shell content query --uri content://settings/secure/android_id --projection value
Row: 0 value=98078XXX96fe
# adb shell settings get secure android_id
98078XXX96fe
```

### SerialNumber
```java
android.os.Build.SERIAL
```

### macAddress
```java
/**
  * <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
  * <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
  * <uses-permission android:name="android.permission.WAKE_LOCK" />
  * */
requestPermission(arrayOf(Manifest.permission.CHANGE_WIFI_STATE), {
    val macAddress: String?
    val wifiManager = applicationContext.getSystemService(Context.WIFI_SERVICE) as WifiManager
    val info = wifiManager.connectionInfo

    if (!wifiManager.isWifiEnabled) {
        //必须先打开，才能获取到MAC地址
        wifiManager.isWifiEnabled = true
        wifiManager.isWifiEnabled = false
    }

    macAddress = info.macAddress

    macAddressBtn.text = "macAddress:${macAddress}"
}, {})

```


### subscriberId
```java
/**
  * <uses-permission android:name = "android.permission.READ_PHONE_STATE" />
  * 
*/
requestPermission(arrayOf(Manifest.permission.READ_PHONE_STATE), {
    val mTelephonyMgr = getSystemService(Context.TELEPHONY_SERVICE) as TelephonyManager
    if (ActivityCompat.checkSelfPermission(this, Manifest.permission.READ_PHONE_STATE) == PackageManager.PERMISSION_GRANTED) {
        val subscriberId = mTelephonyMgr.subscriberId //获取IMSI号
        subscriberIdBtn.text = "SubscriberId:${subscriberId}"
        val deviceId = mTelephonyMgr.deviceId //获取IMSI号
        deviceIdBtn.text = "Device Id:${deviceId}"
        var imei = if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            mTelephonyMgr.imei
        } else {
            ""
        }
        imeiIdBtn.text = "IMEI Id:${imei}"
    }
}, {})
```