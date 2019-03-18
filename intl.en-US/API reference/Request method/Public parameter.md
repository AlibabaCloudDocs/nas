# Public parameter {#concept_62601_zh .concept}

Public request parameters indicate the request parameters that every interface uses.

|Parameter name|Type|Required|Description|
|--------------|----|--------|-----------|
|Format|String|No|Type of the value returned. JSON and XML formats are supported. The default format is JSON.|
|Version|String|Yes|API version number format is in the form of date: YYYY-MM-DD. For this version, it is 2017-06-26.|
|AccessKeyId|String|Yes|The key ID that Alibaba Cloud issues to a user to access services.|
|Signature|String|Yes|The signature result string.|
|SignatureMethod|String|Yes|The signature method. HMAC-SHA1 is currently supported.|
|Timestamp|String|Yes|The time stamp of the request. The date format follows the ISO8601 standard and uses UTC time: YYYY-MM-DDThh:mm:ssZ. For example, 2017-05-26T12:00:00Z.|
|SignatureVersion|String|Yes|Signature algorithm version. The current version is 1.0.|
|SecurityToken|String|No|This value is required to be passed in when you use an STS credential type.|
|SignatureNonce|String|No|The unique random number, used to prevent network replay attacks. You must use different random numbers for different requests.|

## Request example { .section}

```language-shell
GET https://nas.cn-hangzhou.aliyuncs.com/?Action=<Action>
&Format=xml
&Version=2017-06-26
&AccessKeyId=key-test
&Signature=Pc5***3D
&SignatureMethod=HMAC-SHA1
&SignatureNonce=15215528852396
&SignatureVersion=1.0
&Timestamp=2012-06-01T12:00:00Z
…

```

## Public response parameters { .section}

The system returns a unique identification code `RequestId` each time you send a request to call an API whether the call succeeds or does not succeed.

|Parameter name|Type|Description|
|--------------|----|-----------|
|RequestId|Integer|The unique identification code that the system returns.|

## Response example { .section}

-   XML example

    ```language-xml
    <? xml version="1.0" encoding="UTF-8"? >
    <Interface Name + Response>
      <! -- Return Request Tag -->
      <RequestId> 6D9F62C5-BF52-447C-AA34-C77F7AFCCC12</RequestId>
      <! -- Return Result Data -->
    </Interface Name + Response>
    
    ```

-   JSON example

    ```language-json
    {
      "RequestId": "4C467B38-3910-447D-87BC-AC049166F216",
      /* Returned result data */
    }
    
    ```


