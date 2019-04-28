# Android SDK integration guide {#concept_qjr_4vj_n2b .concept}

To integrate the Anti-Bot SDK into your Android app, follow the instructions provided in this topic.

## Android SDK files {#section_h44_z4r_n2b .section}

Contact Customer Services to obtain the correct SDK package. Decompress it on your local machine.

The sdk-Android folder contains the following Android SDK files.

|File|Description|
|----|-----------|
|SecurityGuardSDK-xxx.aar|Main framework|
|AVMPSDK-xxx.aar|VM engine plugin|
|SecurityBodySDK-xxx.aar|Bot recognition plugin|
|yw\_1222\_0335\_mwua.jpg|VM engine configuration file|

## Configure a project {#section_bm1_npr_n2b .section}

Perform the following steps to configure a project:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16085/15564469937355_en-US.png)

1.  Import the .aar files of the Anti-Bot SDK to Android Studio. Copy all the .aar files in the sdk-Android folder to the `libs` directory of the Android app project.

    **Note:** If the `libs` directory does not exist in the current project, manually create a folder named `libs` in the specified path.

2.  Open the build.gradle file of this project and add the following configuration.
    -   Add the `libs` directory as the source for searching dependencies.

        ```
        repositories{
           flatDir {
             dirs 'libs'
           }
        }
        ```

    -   Add compilation dependencies.

        **Note:** The .aar file versions discussed in this topic may be different from those of the files you downloaded.

        ```
        dependencies {
          compile fileTree(include: ['*.jar'], dir: 'libs')
          compile ('com.android.support:appcompat-v7:23.0.0')
          compile (name:'AVMPSDK-external-release-xxx', ext:'aar')
          compile (name:'SecurityBodySDK-external-release-xxx', ext:'aar')
          compile (name:'SecurityGuardSDK-external-release-xxx', ext:'aar')
        }
        ```

3.  Import the .jpg configuration file of the Anti-Bot SDK to the `drawable` directory. Copy the yw\_1222\_0335\_mwua.jpg configuration file in the sdk-Android folder to the `drawable` directory of the Android app project.

    **Note:** If the `drawable` directory does not exist in the current project, manually create a folder named `drawable` in the specified path.

4.  Add “abiFilters” to remove redundant .so files. Currently, the Anti-Bot SDK only provides .so files in the armeabi, armeabi-v7a, and arm64-v8a architectures. Therefore, you must filter the exported ABIs. Otherwise, the app may crash.
    1.  In the libs directory of the Android app project, except for armeabi, armeabi-v7a, and arm64-v8a, delete folders for all the other CPU architectures, including x86, x86\_64, mips, and mips64.
    2.  Add a filter rule in the build.gradle configuration file of the app project. Architectures specified by abiFilters are included in the APK. See the following sample code.

        **Note:** Only the armeabi architecture is specified in the following sample code. You can also specify the armeabi-v7a or arm64-v8a architecture.

        ```
        defaultConfig{
          applicationId "com.xx.yy"
          minSdkVersion xx
          targetSdkVersion xx
          versionCode xx
          versionName "x.x.x"
          ndk {
            abiFilters "armeabi"
            // abiFilters "armeabi-v7a"
            // abiFilters "arm64-v8a"
          }
        }
        ```

        **Note:** If you keep only the .so files in the armeabi architecture, you can remarkably reduce the size of the app without affecting its compatibility.

5.  Configure app permissions.
    -   Assume that the project is an Android Studio project and uses AAR for integration. The relevant permissions have been stated in AAR, so there is no need to configure additional permissions in the project.
    -   For an Eclipse project, you must add the following permissions configuration to the AndroidMenifest.xml file:

        ```
        <uses-permission android:name="android.permission.INTERNET" /> 
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> 
        <uses-permission android:name="android.permission.READ_PHONE_STATE" /> 
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" /> 
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /> 
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" /> 
        <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" /> 
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        ```

6.  Add the ProGuard configuration.

    **Note:** If you have used ProGuard for obfuscation, then you must add the ProGuard configuration. Based on different integration methods, the ProGuard configuration is divided into two types: Eclipse and Android Studio.

    -   **Android Studio**

        The proguard-rules.pro configuration file is used for obfuscation if proguardFiles is configured in build.gradle and minifyEnabled is enabled.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16085/15564469937359_en-US.png)

    -   **Eclipse**

        ProGuard is used for obfuscation if the ProGuard configuration is specified in project.properties \(for example, if project.properties contains the `proguard.config=proguard.cfg` statement\).

        **Note:** Obfuscation is configured in the proguard.cfg file.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16085/15564469937359_en-US.png)

    **Add keep rules**

    To ensure that certain classes are not obfuscated, you must add the following rules in the ProGuard configuration file.

    ```
    -keep class com.taobao.securityjni.**{*;}
    -keep class com.taobao.wireless.security.**{*;}
    -keep class com.ut.secbody.**{*;}
    -keep class com.taobao.dp.**{*;}
    -keep class com.alibaba.wireless.security. **{*;}
    ```


## Develop code {#section_vnw_nrs_n2b .section}

1.  Import the SDK package.

    ```
    import com.alibaba.wireless.security.jaq.JAQException;
    import com.alibaba.wireless.security.jaq.avmp.IJAQAVMPSignComponent;
    import com.alibaba.wireless.security.open.SecurityGuardManager;
    import com.alibaba.wireless.security.open.avmp.IAVMPGenericComponent;
    ```

2.  Initialize the SDK.
    -   **Method definition**: `boolean initialize();`
    -   **Method description**:
        -   Function: initializes the SDK.
        -   Parameter: None.
        -   Return value: Boolean type. true is returned if initialization is successful, whereas false is returned if initialization fails.
    -   **Sample code**:

        ```
        IJAQAVMPSignComponent jaqVMPComp = SecurityGuardManager.getInstance(getApplicationContext()).getInterface(IJAQAVMPSignComponent.class);
        boolean result = jaqVMPComp.initialize();
        ```

3.  Sign the request data.
    -   **Method definition**: `byte[] avmpSign(int signType, byte[] input);`
    -   **Method description**:

        -   Function: signs the input data by using the AVMP technique, and returns the signature string.
        -   Parameters: See the following table.

            |Parameter|Type|Required|Description|
            |---------|----|--------|-----------|
            |signType|Integer|Yes|The algorithm used by the signature. Currently this parameter is fixed, and is set to `3`.|
            |input|byte\[\]|No|The data to be signed, which is generally the entire request body.**Note:** If the request body is empty \(for example, the body of a POST or GET request is empty\), fill in null or the bytes value of an empty string, such as "".getBytes\("UTF-8"\)\).

|

        -   Return value: byte\[\] type. The signature string is returned.
        -   **Sample code**: When the client sends data to the server, it must call the avmpSign method to sign the entire request body data. Then, the signature string wToken is obtained.

            ```
            int VMP_SIGN_WITH_GENERAL_WUA2 = 3;
            String request_body = "i am the request body, encrypted or not!" ;
            byte[] result = jaqVMPComp.avmpSign(VMP_SIGN_WITH_GENERAL_WUA2, request_body.getBytes("UTF-8"));
            String wToken = new String(result, "UTF-8");
            Log.d("wToken", wToken);
            ```

4.  Insert the wToken in the protocol header. Add the content of the wToken field to the HttpURLConnection class object.

    Sample code:

    ```
    String request_body = "i am the request body, encrypted or not!" ;
    URL url = new URL("http://www.xxx.com");
    HttpURLConnection conn = (HttpURLConnection) url.openConnection();
    conn.setRequestMethod("POST");
    // set wToken info to header 
    conn.setRequestProperty("wToken", wToken);
    OutputStream os = conn.getOutputStream();
    // set request body info
    byte[] requestBody = request_body.getBytes("UTF-8");
    os.write(requestBody);
    os.flush();
    os.close();
    ```

5.  Send data to the server. Send the data with the modified protocol header to the server mapping the app. Anti-Bot Service captures the data and parses the wToken for risk identification.

**Warning:** The signed request body must be consistent with the request body that is actually sent by the client. That is, the string coding format, spaces, special characters, and parameter sequence of the signed request body must be consistent with those of the request body actually sent by the client. Otherwise, signature verification may fail.

## Error codes {#section_frr_lts_n2b .section}

If you call the initialize and avmpSigni methods, exceptions may occur. If an exception or error occurs when generating the signature string, search `SecException` for related information in the log.

**Common error codes and definitions**

|Error code|Description|
|----------|-----------|
|1901|Incorrect parameter value. Enter the correct parameter value.|
|1902|Image file error. The APK signature used to retrieve the image file is inconsistent with the current app's APK signature. Generate a new image file by using the current app's APK.|
|1903|Incorrect image file format.|
|1904|Upgrade to the latest image version. The AVMP signature function only supports v5 images.|
|1905|Unable to find the image file. Make sure that the image file is in the res\\drawable directory. The AVMP image is yw\_1222\_0335\_mwua.jpg.|
|1906|byteCode corresponding to the AVMP signature is missing from the image. Check whether the image is correct.|
|1907|Failed to initialize AVMP. Try again later.|
|1910|Invalid avmpInstance instance. Possible causes are as follows:-   InvokeAVMP is called after AVMPInstance is destroyed.
-   The byteCode version of the image does not match that of the SDK.

|
|1911|byteCode of the encrypted image does not have the corresponding export function.|
|1912|AVMP call fails. Submit a ticket for further assistance.|
|1913|InvokeAVMP is called after AVMPInstance is destroyed.|
|1915|Insufficient AVMP memory. Try again later.|
|1999|Unknown error. Try again later.|

## Test and verify the effect of integration {#section_mq3_g5s_n2b .section}

Perform the following steps to verify that your app has been correctly integrated with the Anti-Bot SDK:

1.  Convert the packaged APK file into a ZIP file by modifying the file name extension, and decompress the file on your local machine.
2.  Go to the libs directory of the project, and make sure that the folder only contains the armeabi, armeabi-v7a, and arm64-v8a subfolders.

    **Note:** If you find folders for other architectures, delete them. For more information, see [Delete folders for other architectures](intl.en-US/User Guide/App protection/Android SDK integration guide.md#section_bm1_npr_n2b).

3.  Go to the res/drawable directory of the project, and make sure that the yw\_1222\_0335\_mwua.jpg file exists and that its size is not 0.
4.  Print the log, and make sure that the correct signature information is generated after the avmpSign method is called.

    **Note:** If the signature information is not generated, see the error messages to resolve the problem.


## FAQ {#section_yzl_cvs_n2b .section}

**Why is the key image incorrectly optimized after shrinkResources is specified?**

In Android Studio, if shrinkResources is set to true, resource files that are not referenced in the code may be optimized during project compilation. This operation may corrupt the .jpg file in the Anti-Bot SDK. If the size of the yw\_1222\_0335.jpg configuration file in the packaged APK is 0 KB, the image file has been optimized.

**Solution**

1.  Create a directory named raw in the res directory of the project, and create a file named keep.xml in the raw directory.
2.  Add the following content to the keep.xml file:

    ```
    <? xml version="1.0" encoding="utf-8"? >
    <resources xmlns:tools="http://schemas.android.com/tools"
    tools:keep="@drawable/yw_1222_0335.jpg,@drawable/yw_1222_0335_mwua.jpg" />
    ```

3.  After adding the content, re-compile the project APK.

