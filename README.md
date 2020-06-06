# Add Security Exception to APK

In Android 7.0, Google introduced changes to the way user Certificate Authorities (CA) are trusted. These changes prevent third-parties from listening to network requests coming out of the application:
More info: 
1) https://developer.android.com/training/articles/security-config.html
2) http://android-developers.blogspot.com/2016/07/changes-to-trusted-certificate.html

This script injects into the APK network security exceptions that allow third-party software like Charles Proxy/Fiddler to listen to the network requests and responses of some Android applications.

## For HTTPS and HTTP tracing 

https://mitmproxy.org/

## Getting Started

Download the script and the XML file and place them in the same directory.

### Prerequisites
APKTOOL is not needed anymore.

~~You will need `apktool` and the Android SDK installed~~

~~I recommend using `brew` on Mac to install `apktool`:~~

~~```brew install apktool```~~

Install JDK

```
sudo apt install default-jdk
```

## Usage

The script take two arguments: 
1) APK file path.
2) keystore file path (**optional** - Default is: ~/.android/debug.keystore )

### Examples

```
./addSecurityExceptions.sh myApp.apk

or

./addSecurityExceptions.sh myApp.apk ~/.android/debug.keystore

```

### Possible Errors 

```
W: /tmp/instake/AndroidManifest.xml:1: error: No resource identifier found for attribute 'compileSdkVersion' in package 'android'
W: 
W: /tmp/instake/AndroidManifest.xml:1: error: No resource identifier found for attribute 'compileSdkVersionCodename' in package 'android'
W: 
W: /tmp/instake/AndroidManifest.xml:10: error: No resource identifier found for attribute 'appComponentFactory' in package 'android'
W: 
brut.androlib.AndrolibException: brut.common.BrutException: could not exec (exit code = 1): [/tmp/brut_util_Jar_1366784670753768586.tmp, p, --forced-package-id, 127, --min-sdk-version, 16, --target-sdk-version, 28, --version-code, 35, --version-name, 1.3.5, --no-version-vectors, -F, /tmp/APKTOOL10223395514992124954.tmp, -e, /tmp/APKTOOL22757546043127297.tmp, -0, arsc, -I, /tmp/1.apk, -S, /tmp/instake/res, -M, /tmp/instake/AndroidManifest.xml]
jarsigner: unable to open jar file: ./instake_new.apk
```

**Solutions**
```
sudo apt-get install apktool
apktool empty-framework-dir --force
rm -rf /tmp/1.apk 

```