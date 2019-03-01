# iOS SDK integration guide {#concept_zbh_nvj_n2b .concept}

To integrate the Anti-Bot SDK into your iOS app, follow the instructions provided in this topic.

## iOS SDK files {#section_b2d_wrm_n2b .section}

Contact the technical support team for Anti-Bot Service to obtain the correct SDK package. Decompress it on your local machine.

The sdk-iOS folder contains the following iOS SDK files.

|File|Description|
|----|-----------|
|SGMain.framework|Main framework|
|SecurityGuardSDK.framework|Basic security plugin|
|SGSecurityBody.framework|Bot recognition plugin|
|SGAVMP.framework|VM plugin|
|yw\_1222\_0335\_mwua.jpg|Configuration file|

## Configure a project {#section_jjl_ksm_n2b .section}

Perform the following steps to configure a project for your app:

1.  Add frameworks. Add the four `.framework` files in the Anti-Bot SDK package to the dependent library of the iOS app project.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16084/15514371127375_en-US.png)

2.  Add other linker flags.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16084/15514371137376_en-US.png)

3.  Add the following system dependent libraries.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16084/15514371137377_en-US.png)

4.  Import the configuration file. Add the `yw_1222_0335_mwua.jpg` configuration file in the SDK package to the `mainbunle` directory.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16084/15514371137378_en-US.png)

    **Note:** When the app integrates multiple targets, make sure to add the `w_1222_0335_mwua.jpg` configuration file to the correct Target Membership.


## Develop code {#section_dwq_3xs_n2b .section}

1.  Initialize the SDK.
    -   **Interface definition**: `+ (BOOL) initialize;`
    -   **Interface description**:
        -   Function: Initializes the SDK.
        -   Parameter: None.
        -   Return value: Boolean type. YES is returned if initialization is successful, whereas NO is returned if initialization fails.
    -   **Call method**: `[JAQAVMPSignature initialize];`
    -   **Sample code**:

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

2.  Sign the request data.
    -   **Interface definition**: `+ (NSData*) avmpSign: (NSInteger) signType input: (NSData*) input;`
    -   **Interface description**:
        -   Function: Signs the input data by using the AVMP technique, and returns the signature string.

            **Warning:** The signed request body must be consistent with the request body that is actually sent by the client. That is, the string coding format, spaces, special characters, and parameter sequence of the signed request body must be consistent with those of the request body actually sent by the client. Otherwise, signature verification may fail.

        -   Parameters: See the following table.

            |Parameter|Type|Required|Description|
            |---------|----|--------|-----------|
            |signType|NSInteger|Yes|The algorithm used by the signature. Currently this parameter is fixed, and is set to `3`.|
            |input|NSData\*|No|The data to be signed, which is generally the entire request body.**Note:** If the request body is empty \(for example, the body of a POST or GET request is empty\), enter null or the bytes value of an empty string.

|

        -   Return value: NSData\* type. The signature string is returned.
    -   **Call method**: `[JAQAVMPSignature avmpSign: 3 input: request_body];`
    -   **Sample code**:

        **Note:** When the client sends data to the server, it must call the avmpSign interface to sign the entire request body. Then, the signature string wToken is obtained.

        ```
        # define VMP_SIGN_WITH_GENERAL_WUA2 (3)
        - (NSString*) avmpSign{
          @synchronized(self) {
            NSString* request_body = @"i am the request body, encrypted or not!" ;
            if(![ self initAVMP]){
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

        **Note:** Even if the request body is empty, the client still must call the avmpSign interface to generate the wToken. In this case, directly use null as the second parameter.

        ```
        NSData* sign = [JAQAVMPSignature avmpSign: VMP_SIGN_WITH_GENERAL_WUA2 input:nil];
        ```

3.  Insert the wToken in the protocol header.

    **Sample code**

    ```
    #define VMP_SIGN_WITH_GENERAL_WUA2 (3)
    -(void)setHeader
    { NSString* request_body = @"i am the request body, encrypted or not!" ;
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

4.  Send data to the server mapping the app. Send the data with the modified protocol header to Anti-Bot Service, which parses the wToken for risk identification and malicious request interception, and then forwards legitimate requests to the mapping server.

## Error codes {#section_hzy_rzs_n2b .section}

Calling of the initialize and avmpSign interfaces may encounter exceptions. If an exception or error occurs when generating the signature string, search `SG Error` for related information in the console.

**Common error codes and definitions**

|Error code|Definition|
|----------|----------|
|1901|Incorrect parameter value. Enter the correct parameter value.|
|1902|Image file error. BundleID mismatch.|
|1903|Incorrect image file format.|
|1904|Upgrade to the latest image version. The AVMP signature function only supports v5 images.|
|1905|Unable to find the image file. Make sure that the yw\_1222\_0335\_mwua.jpg image file has been correctly added in the project.|
|1906|byteCode corresponding to the AVMP signature is missing from the image. Check whether the image is correct.|
|1907|Failed to initialize AVMP. Try again later.|
|1910|Invalid avmpInstance instance. Possible causes are as follows:-   InvokeAVMP is called after AVMPInstance is destroyed.
-   The byteCode version of the image does not match that of the SDK.

|
|1911|byteCode of the encrypted image does not have the corresponding export function.|
|1912|The AVMP call failed. Submit a ticket for help.|
|1913|InvokeAVMP is called after AVMPInstance is destroyed.|
|1915|Insufficient memory during the AVMP call. Try again later.|
|1999|Unknown error. Try again later.|

