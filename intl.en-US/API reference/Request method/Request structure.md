# Request structure {#concept_62600_zh .concept}

NAS API requests are in a unified structure.

## Endpoint {#section_pvr_qdf_hfb .section}

The endpoint of NAS APIs follows a format of `nas.aliyuncs.com` and `nas. [RegionId.]aliyuncs.com`.

Specifically, `RegionId` refers to the service region. You can call the API of the designated region based on your own region. The service is available in the following regions.

|Region|RegionId|Endpoint|
|------|--------|--------|
|Beijing|cn-beijing|nas.cn-beijing.aliyuncs.com|
|Shanghai|cn-shanghai|nas.cn-shanghai.aliyuncs.com|
|Hangzhou|cn-hangzhou|nas.cn-hangzhou.aliyuncs.com|
|Shenzhen|cn-shenzhen|nas.cn-shenzhen.aliyuncs.com|

## Communication protocol { .section}

HTTP and HTTPS protocols are supported for request communications. We recommend that you use an HTTPS channel which provides higher security.

## Request methods { .section}

NAS API supports sending HTTP GET requests. Using this method, you are required to include request parameters in the request URL.

## Request parameters { .section}

Each request must specify the operation to be executed, namely the Action parameter \(such as `DescribeRegions`\). Each operation must contain the common request parameters and the specific request parameters of the specified operation.

## Character encoding { .section}

Requests and responses are both encoded using the `UTF-8` character set.

## Use SDK { .section}

JAVA, PHP, and, Python SDKs are currently supported.

We recommend that you use SDKs which can simplify the process for HTTP message encapsulation and signature operations.

You can download the SDK from the following links:

-   Java: [NAS Java SDK](https://github.com/aliyun/aliyun-openapi-java-sdk/tree/master/aliyun-java-sdk-nas)
-   Python: [NAS Python SDK](https://github.com/aliyun/aliyun-openapi-python-sdk/tree/master/aliyun-python-sdk-nas)
-   PHP: [NAS PHP SDK](https://github.com/aliyun/aliyun-openapi-php-sdk/tree/master/aliyun-php-sdk-nas)
-   .Net: [NAS .Net SDK](https://github.com/aliyun/aliyun-openapi-net-sdk/tree/master/aliyun-net-sdk-nas)

