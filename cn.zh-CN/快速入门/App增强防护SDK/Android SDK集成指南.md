# Android SDK集成指南 {#concept_qjr_4vj_n2b .concept}

参考以下SDK集成说明将您的Android App集成Anti-Bot SDK。

## Android SDK文件说明 {#section_h44_z4r_n2b .section}

联系爬虫风险管理技术支持人员获取对应的SDK包，解压至本地。

在sdk-Android文件夹中，包含以下Android SDK文件：

|文件|说明|
|--|--|
|SecurityGuardSDK-xxx.aar|主框架SDK文件|
|AVMPSDK-xxx.aar|虚拟机引擎插件|
|SecurityBodySDK-xxx.aar|人机识别插件|
|yw\_1222\_0335\_mwua.jpg|虚拟机引擎配置文件|

## 项目工程配置 {#section_bm1_npr_n2b .section}

参考以下步骤，完成项目工程配置：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16085/15447812427355_zh-CN.png)

1.  在Android Studio中导入Anti-Bot SDK的aar文件。将sdk-Android文件夹中所有aar文件复制到Android App工程项目的`libs`目录中。

    **说明：** 如果当前工程项目中不存在`libs`目录，在指定路径下手工创建`libs`文件夹。

2.  打开该Module的build.gradle文件，增加以下配置信息。
    -   将`libs`目录添加为查找依赖的源。

        ```
        repositories{
           flatDir {
             dirs 'libs'
           }
        }
        ```

    -   添加编译依赖。

        **说明：** aar文件的版本号可能有所不同，以您下载解压得到的文件名为准。

        ```
        dependencies {
          compile fileTree(include: ['*.jar'], dir: 'libs')
          compile ('com.android.support:appcompat-v7:23.0.0')
          compile (name:'AVMPSDK-external-release-xxx', ext:'aar')
          compile (name:'SecurityBodySDK-external-release-xxx', ext:'aar')
          compile (name:'SecurityGuardSDK-external-release-xxx', ext:'aar')
        }
        ```

3.  将Anti-Bot SDK的jpg配置文件导入`drawable`目录。将sdk-Android文件夹中的yw\_1222\_0335\_mwua.jpg配置文件复制到Android App工程项目的`drawable`目录中。

    **说明：** 如果当前工程项目中不存在`drawable`目录，在指定路径下手工创建`drawable`文件夹。

4.  过滤ABI（删除多余架构SO）。Anti-Bot SDK目前仅支持armeabi、armeabi-v7a、arm64-v8a架构的SO。因此，您需要对最终导出的ABI进行过滤。否则，可能导致App崩溃。
    1.  在Android App工程的lib目录中，删除除armeabi、armeabi-v7a、arm64-v8a文件夹外所有其他CPU架构的文件夹，包括x86、x86\_64、mips、mips64等，只保留armeabi、armeabi-v7a、arm64-v8a文件夹。
    2.  参考以下代码示例，在App工程的build.gradle配置文件中增加过滤规则，被abiFilters指定的架构将会被包含在APK文件中。

        **说明：** 本代码示例中仅指定了armeabi架构，您可以根据实际情况指定或兼容armeabi-v7a、arm64-v8a架构。

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

        **说明：** 只保留armeabi架构的SO，不会影响App的兼容性，还能大幅减小App的体积。

5.  添加App权限。
    -   如果是Android Studio项目，并且使用aar方式进行集成。由于在aar中已经声明了相关权限，因此不需要在项目中额外配置权限。
    -   如果是Eclipse项目，您需要在AndroidMenifest.xml文件中添加以下权限配置：

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

6.  添加ProGuard配置。

    **说明：** 如果您使用了Proguard进行混淆，则需要添加ProGuard配置。ProGuard的配置根据集成方式的不同，分为Eclipse和Android Studio两种情况。

    -   **Android Studio**

        如果在build.gradle中配置了proguardFiles，并且开启了minifyEnabled，则表明使用了proguard-rules.pro配置文件进行混淆。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16085/15447812437359_zh-CN.png)

    -   **Eclipse**

        如果在project.properties中指定了proguard配置，例如在project.properties中存在`proguard.config=proguard.cfg`语句，则表明使用了proguard进行混淆。

        **说明：** 混淆配置在proguard.cfg 文件中。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16085/15447812437359_zh-CN.png)

    **添加keep规则**

    为了保证一些需要的类不被混淆，需要在proguard的配置文件中添加以下规则：

    ```
    -keep class com.taobao.securityjni.**{*;}
    -keep class com.taobao.wireless.security.**{*;}
    -keep class com.ut.secbody.**{*;}
    -keep class com.taobao.dp.**{*;}
    -keep class com.alibaba.wireless.security.**{*;}
    ```


## 代码编写 {#section_vnw_nrs_n2b .section}

1.  导入包。

    ```
    import com.alibaba.wireless.security.jaq.JAQException;
    import com.alibaba.wireless.security.jaq.avmp.IJAQAVMPSignComponent;
    import com.alibaba.wireless.security.open.SecurityGuardManager;
    import com.alibaba.wireless.security.open.avmp.IAVMPGenericComponent;
    ```

2.  初始化。
    -   **接口定义**：`boolean initialize();`
    -   **接口描述**：
        -   功能：初始化SDK。
        -   参数：无。
        -   返回值：Boolean类型。初始化成功返回true，失败返回false。
    -   **示例代码**：

        ```
        IJAQAVMPSignComponent jaqVMPComp = SecurityGuardManager.getInstance(getApplicationContext()).getInterface(IJAQAVMPSignComponent.class);
        boolean result = jaqVMPComp.initialize();
        ```

3.  签名请求数据。
    -   **接口定义**：`byte[] avmpSign(int signType, byte[] input);`
    -   **接口描述**：

        -   功能：使用avmp技术对input的数据进行签名处理，并且返回签名串。
        -   参数：详见下表。

            |参数名|类型|是否必须|说明|
            |---|--|----|--|
            |signType|int|是|签名使用的算法。目前是固定值，填写`3`。|
            |input|byte\[\]|否|待签名的数据，一般是整个请求体（request body）。**说明：** 如果请求体为空（例如POST请求的body为空、或者GET请求），则填写空对象null或空字符串的Bytes值（例如，"".getBytes\("UTF-8"\)\)。

|

        -   返回值：byte\[\]类型，返回签名串。
        -   **示例代码**：客户端向服务器端发送数据时，需要调用avmpSign接口对整个body数据进行签名处理，所得到的签名串就是wToken。

            ```
            int VMP_SIGN_WITH_GENERAL_WUA2 = 3;
            String request_body = "i am the request body, encrypted or not!";
            byte[] result = jaqVMPComp.avmpSign(VMP_SIGN_WITH_GENERAL_WUA2, request_body.getBytes("UTF-8"));
            String wToken = new String(result, "UTF-8");
            Log.d("wToken", wToken);
            ```

4.  将wToken放进协议头。在HttpURLConnection类的对象中添加wToken字段的内容。

    示例代码：

    ```
    String request_body = "i am the request body, encrypted or not!";
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

5.  发送数据到服务器。将修改好协议头的数据发送到App自有服务器，中间会由Anti-Bot截获，并通过解析wToken进行风险识别。

**警告：** 被签名的请求体应该与客户端实际发送的请求体完全一致。完全一致的含义包括请求体中字符串的编码格式、空格、特殊字符以及参数的顺序等均一致，否则将导致签名验证失败。

## 错误码 {#section_frr_lts_n2b .section}

上述initialize和avmpSign接口的调用过程中可能出现异常。如果生成签名串异常或失败，搜索Log中与`SecException` 相关的信息。

**常见错误码及含义**

|错误代码|含义|
|----|--|
|1901|参数不正确，请检查输入的参数。|
|1902|图片文件有问题。一般是获取图片文件时的APK签名和当前程序的APK签名不一致。请使用当前程序的APK重新生成图片。|
|1903|图片文件格式有问题。|
|1904|请升级新版本图片。AVMP签名功能仅支持V5图片。|
|1905|没有找到图片文件。请确保图片文件在res\\drawable目录下，与AVMP相关的图片为yw\_1222\_0335\_mwua.jpg。|
|1906|图片中缺少AVMP签名对应的byteCode。请检查使用的图片是否正确。|
|1907|初始化AVMP失败，请重试。|
|1910|非法的avmpInstance实例。可能由于以下原因导致：-   AVMPInstance被destroy后，调用InvokeAVMP。
-   图片byteCode版本与SDK不匹配。

|
|1911|加密图片的byteCode没有相应导出的函数。|
|1912|AVMP调用失败。请联系我们。|
|1913|AVMPInstance被destroy后，调用InvokeAVMP出现该错误。|
|1915|AVMP调用内存不足，请重试。|
|1999|未知错误，请重试。|

## 集成效果确认 {#section_mq3_g5s_n2b .section}

参考以下步骤，确认您的App已正确集成Anti-Bot SDK：

1.  将打包生成的APK文件通过修改扩展名的方式转换成ZIP压缩文件，并将该压缩文件解压至本地。
2.  定位到工程的lib目录，确保文件夹中只存在armeabi、armeabi-v7a、arm64-v8a文件夹。

    **说明：** 如果存在其他架构的文件夹，参考[项目工程配置](cn.zh-CN/快速入门/App增强防护SDK/Android SDK集成指南.md#section_bm1_npr_n2b)移除其它架构的文件夹。

3.  定位到工程的res/drawable目录，确认存在yw\_1222\_0335\_mwua.jpg文件，且文件大小不为0。
4.  通过打印日志，确保调用avmpSign接口后能生成正确的签名信息。

    **说明：** 如果签名信息未生成，参考错误码信息进行排查。


## 常见问题 {#section_yzl_cvs_n2b .section}

**指定shrinkResources后，密钥图片被错误地优化**

在Android Studio中，如果指定shrinkResources为true，在工程编译时可能对未在代码中引用的资源文件进行优化。该操作可能导致Anti-Bot SDK中的jpg文件无法正常工作。如果打包后得到APK中，yw\_1222\_0335.jpg配置文件的大小为0KB，则表明该图片文件已被优化。

**解决方法**

1.  在工程的res目录中新建raw目录，并在raw目录中创建keep.xml文件。
2.  在keep.xml文件中，添加以下内容：

    ```
    <?xml version="1.0" encoding="utf-8"?>
    <resources xmlns:tools="http://schemas.android.com/tools"
    tools:keep="@drawable/yw_1222_0335.jpg,@drawable/yw_1222_0335_mwua.jpg" />
    ```

3.  添加完成后，重新编译工程APK即可。

