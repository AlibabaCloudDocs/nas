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
|Qingdao|cn-qingdao|nas.cn-qingdao.aliyuncs.com|
|Zhangjiakou|cn-zhangjiakou|nas.cn-zhangjiakou.aliyuncs.com|
|Hohhot|cn-huhehaote|nas.cn-huhehaote.aliyuncs.com|
|Chengdu|cn-chengdu|nas.cn-chengdu.aliyuncs.com|
|China \(Hong Kong\)|cn-hongkong|nas.cn-hongkong.aliyuncs.com|
|Singapore|ap-southeast-1|nas.ap-southeast-1.aliyuncs.com|
|Sydney|ap-southeast-2|nas.ap-southeast-2.aliyuncs.com|
|Kuala Lumpur|ap-southeast-3|nas.ap-southeast-3.aliyuncs.com|
|Jakarta|ap-southeast-5|nas.ap-southeast-5.aliyuncs.com|
|Tokyo|ap-northeast-1|nas.ap-northeast-1.aliyuncs.com|
|Mumbai|ap-south-1|nas.ap-south-1.aliyuncs.com|
|Frankfurt|eu-central-1|nas.eu-central-1.aliyuncs.com|
|London|eu-west-1|nas.eu-west-1.aliyuncs.com|
|Silicon Valley|us-west-1|nas.us-west-1.aliyuncs.com|
|Virginia|us-east-1|nas.us-east-1.aliyuncs.com|

## Communication protocol {#section_mbx_84u_ucp .section}

HTTP and HTTPS protocols are supported for request communications. We recommend that you use an HTTPS channel which provides higher security.

## Request methods {#section_xc0_uu5_4pv .section}

NAS API supports sending HTTP GET requests. Using this method, you are required to include request parameters in the request URL.

## Request parameters {#section_rbp_42i_e7m .section}

Each request must specify the operation to be executed, namely the Action parameter \(such as `DescribeRegions`\). Each operation must contain the common request parameters and the specific request parameters of the specified operation.

## Character encoding {#section_zwo_d83_hv2 .section}

Requests and responses are both encoded using the `UTF-8` character set.

## Use SDK {#section_qu8_czu_lrp .section}

JAVA, PHP, and, Python SDKs are currently supported.

We recommend that you use SDKs which can simplify the process for HTTP message encapsulation and signature operations.

You can download the SDK from the following links:

-   Java: [NAS Java SDK](https://github.com/aliyun/aliyun-openapi-java-sdk/tree/master/aliyun-java-sdk-nas)
-   Python: [NAS Python SDK](https://github.com/aliyun/aliyun-openapi-python-sdk/tree/master/aliyun-python-sdk-nas)
-   PHP: [NAS PHP SDK](https://github.com/aliyun/aliyun-openapi-php-sdk/tree/master/aliyun-php-sdk-nas)
-   .Net: [NAS .Net SDK](https://github.com/aliyun/aliyun-openapi-net-sdk/tree/master/aliyun-net-sdk-nas)

