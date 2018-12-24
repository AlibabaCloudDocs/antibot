# iOS SDK集成指南 {#concept_zbh_nvj_n2b .concept}

参考以下SDK集成说明将您的iOS App集成Anti-Bot SDK。

## iOS SDK文件说明 {#section_b2d_wrm_n2b .section}

联系爬虫风险管理技术支持人员获取对应的SDK包，解压至本地。

在sdk-iOS文件夹中，包含以下iOS SDK文件：

|文件|说明|
|--|--|
|SGMain.framework|主框架SDK文件|
|SecurityGuardSDK.framework|基础安全插件|
|SGSecurityBody.framework|人机识别插件|
|SGAVMP.framework|虚拟机插件|
|yw\_1222\_0335\_mwua.jpg|配置文件|

## 项目工程配置 {#section_jjl_ksm_n2b .section}

参考以下步骤，为您的App项目工程配置：

1.  添加Framework。将Anti-Bot SDK包中的四个`.framework`文件添加到iOS App工程的依赖库中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16084/15447812357375_zh-CN.png)

2.  添加链接选项。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16084/15447812357376_zh-CN.png)

3.  添加以下系统依赖库。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16084/15447812357377_zh-CN.png)

4.  引入配置文件。将SDK包中的`yw_1222_0335_mwua.jpg`配置文件加至 `mainbunle`目录。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16084/15447812357378_zh-CN.png)

    **说明：** 在应用集成多个target的情况下，确认将`yw_1222_0335_mwua.jpg`配置文件加入到正确的Target Membership中。


## 代码编写 {#section_dwq_3xs_n2b .section}

1.  初始化SDK。
    -   **接口定义**：`+ (BOOL) initialize;`
    -   **接口描述**：
        -   功能：初始化SDK。
        -   参数：无。
        -   返回值：BOOL类型。初始化成功返回YES，失败返回NO。
    -   **调用方式**：`[JAQAVMPSignature initialize];`
    -   **代码示例**：

        ```
        static BOOL avmpInit = NO;
        - (BOOL) initAVMP{
          @synchronized(self) { // just initialize once
            if(avmpInit == YES){
              return YES; 
            }
            avmpInit = [JAQAVMPSignature initialize];
            return avmpInit; 
          }
        }
        ```

2.  签名请求数据。
    -   **接口定义**：`+ (NSData*) avmpSign: (NSInteger) signType input: (NSData*) input;`
    -   **接口描述**：
        -   功能：使用avmp技术对input的数据进行签名处理，并返回签名串。

            **警告：** 被签名的请求体应该与客户端实际发送的请求体完全一致。完全一致的含义包括请求体中字符串的编码格式、空格、特殊字符以及参数的顺序等均一致，否则将导致签名验证失败。

        -   参数：详见下表。

            |参数名|类型|是否必须|说明|
            |---|--|----|--|
            |signType|NSInteger|是|签名使用的算法。目前是固定值，填写`3`。|
            |input|NSData\*|否|待签名的数据，一般是整个请求体（request body）。**说明：** 如果请求体为空（例如POST请求的body为空、或者GET请求），则填写空对象null或空字符串的Bytes值。

|

        -   返回值：NSData\*类型，返回签名串。
    -   **调用方式**：`[JAQAVMPSignature avmpSign: 3 input: request_body];`
    -   **代码示例**：

        **说明：** 客户端向服务器端发送数据时，需要调用avmpSign接口对整个body数据进行签名处理，所得到的签名串就是wToken。

        ```
        # define VMP_SIGN_WITH_GENERAL_WUA2 (3)
        - (NSString*) avmpSign{
          @synchronized(self) {
            NSString* request_body = @"i am the request body, encrypted or not!";
            if(![self initAVMP]){
              [self toast:@"Error: init failed"];
                return nil;
            }
            NSString* wToken = nil;
            NSData* data = [request_body dataUsingEncoding:NSUTF8StringEncoding];
            NSData* sign = [JAQAVMPSignature avmpSign: VMP_SIGN_WITH_GENERAL_WUA2 input:data];
            if(sign == nil || sign.length <= 0){
              return nil;
            }else{
              wToken = [[NSString alloc] initWithData:sign encoding: NSUTF8StringEncoding];
              return wToken;
            }
          }
        }
        ```

        **说明：** 如果请求体为空，仍需要调用avmpSign接口生成wToken，第二个参数直接传入空值即可。

        ```
        NSData* sign = [JAQAVMPSignature avmpSign: VMP_SIGN_WITH_GENERAL_WUA2 input:nil];
        ```

3.  将wToken放进协议头。

    **代码示例**

    ```
    #define VMP_SIGN_WITH_GENERAL_WUA2 (3)
    -(void)setHeader
    { NSString* request_body = @"i am the request body, encrypted or not!";
      NSData* body_data = [request_body dataUsingEncoding:NSUTF8StringEncoding];
      NSString* wToken = nil;
      NSData* sign = [JAQAVMPSignature avmpSign: VMP_SIGN_WITH_GENERAL_WUA2 input:body_data];
      wToken = [[NSString alloc] initWithData:sign encoding: NSUTF8StringEncoding];
      NSString *strUrl = [NSString stringWithFormat:@"http://www.xxx.com/login"];
      NSURL *url = [NSURL URLWithString:strUrl];
      NSMutableURLRequest *request =
        [[NSMutableURLRequest alloc]initWithURL:url cachePolicy:NSURLRequestReloadIgnoringCacheData timeoutInterval:20];
      [request setHTTPMethod:@"POST"];
      // set request body info
      [request setHTTPBody:body_data];
      // set wToken info to header
      [request setValue:wToken forHTTPHeaderField:@"wToken"];
      NSURLConnection *mConn = [[NSURLConnection alloc]initWithRequest:request delegate:self startImmediately:true];
      [mConn start]; 
      // ...
    }
    ```

4.  发送数据到服务器。将修改好协议头的数据发送到Anti-Bot，通过解析wToken进行风险识别、拦截恶意请求，然后将合法请求转发回源站。

## 错误码 {#section_hzy_rzs_n2b .section}

上述initialize和avmpSign接口的调用过程中可能出现异常。如果生成签名串异常或失败，在console中搜索与`SG Error`相关的错误码信息。

**常见错误代码及含义**

|错误代码|含义|
|----|--|
|1901|参数不正确，请检查输入的参数。|
|1902|图片文件错误。可能是由于BundleID不匹配导致。|
|1903|图片文件格式有问题。|
|1904|请升级新版本图片。AVMP签名功能仅支持v5图片。|
|1905|无法找到图片文件。请确保图片文件yw\_1222\_0335\_mwua.jpg已正确添加在工程中。|
|1906|图片中缺少AVMP签名对应的byteCode。请检查使用的图片是否正确。|
|1907|初始化AVMP失败，请重试。|
|1910|非法的avmpInstance实例。可能由于以下原因导致：-   AVMPInstance被destroy后，调用InvokeAVMP。
-   图片byteCode版本与SDK不匹配。

|
|1911|加密图片的byteCode没有相应导出的函数。|
|1912|AVMP调用失败，请联系我们。|
|1913|AVMPInstance被destroy后，调用InvokeAVMP时出现该错误。|
|1915|AVMP调用内存不足，请重试。|
|1999|未知错误，请重试。|

