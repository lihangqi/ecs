# Signature {#EcsApiSignature .reference}

We perform the sender authentication for each request. Therefore, a signature information must be included in the request, irrespective of the use of HTTP or HTTPS protocol. By using the AccessKeyID and AccessKeySecret, we perform symmetric encryption to authenticate the sender request.

The AccessKey is equivalent to a logon password. However, an AccessKey is used to call APIs, while the logon password is used to log on to the [ECS console](https://ecs.console.aliyun.com/). Where an AccessKeyID is the visitor identity, an AccessKeySecret is the secret key to encrypt the signature string and to verify the signature string sent to our server. You must keep your AccessKey confidential to prevent possible data breach event.

**Note:** We provide SDKs and third-party SDKs for multiple programming languages to help you skip the authentication process. For more information, see [SDK](https://github.com/aliyun).

## Step 1. Compose a standardized request URL {#section_czy_tyb_wdb .section}

1.  Sort the request parameters in a lexicographical order. The request parameters include the API-specific parameters and [common request parameters](intl.en-US/API Reference/Call methods/Common parameters.md#commonRequestParameters) except for the `Signature` parameter.

    **Note:** For example, if you make a request by using the GET method, these parameters are in the section of the URL followed by a question mark `?` and connected by ampersands `&`.

2.  Encode the request parameters by using the UTF-8 character set and according to the [RFC3986](http://tools.ietf.org/html/rfc3986) rules.
    -   Do not encode the A~Z and a~z characters, numbers \(0~9\), hyphens `-`, underscores `_`, periods `.`, and tildes `~` .

    -   Encode other characters in the `%XY` format, with `XY` representing the hexadecimal ASCII value of the characters. For example, the half-width double quotes \(`"`\) are encoded as `%22`.

    -   Encode the extended UTF-8 characters in `%XY%ZA…` format.

    -   Encode the whitespaces \( \) to `%20` instead of the plus signs \(`+`\).

        Alternatively, you can use libraries that support the `application/x-www-form-urlencoded` MIME-type URL encoding,

        for example the `java.net.URLEncoder` of Java language. If so, use the `percentEncode` Java method, in the encoded strings, replace the plus signs \(`+`\) with `%20`, the asterisks \(`*`\) with `%2A`, and `%7E` to the tildes \(`~`\). See the following example:

        ```
        
        private static final String ENCODING = "UTF-8";
        private static String percentEncode(String value) throws UnsupportedEncodingException {
        return value ! = null ? URLEncoder.encode(value, ENCODING).replace("+", "%20").replace("*", "%2A").replace("%7E", "~") : null;
        }
        ```

3.  Connect the encoded parameters and their values with the equal signs \(`=`\).
4.  Concatenate the encoded parameters with ampersands \(`&`\).

Now, you get a canonicalized query string, and its structure must be the same as described in the topic [Request structure](intl.en-US/API Reference/Call methods/Request structure.md#).

## Step 2. Construct a signature string {#StringToSign .section}

1.  Create a variable `StringToSign` by using the canonicalized query string. You can use the aforementioned `[percentEncode](#percentEncode)` to handle the standardization request string that was constructed by the previous steps, with the following rules:

    ```
    
    StringToSign=
      HTTPMethod + "&" + //HTTPMethod: HTTP method used for making request, for example GET.
      percentEncode("/") + "&" + //percentEncode("/"): Encode backslash (/) to %2F.
      percentEncode(CanonicalizedQueryString) //Encode the canonicalized query string created in the Step 1.
    ```

2.  Create a variable Signature by calculating the HMAC-SHA1 value of the `StringToSign` according to the [RFC2104](http://www.ietf.org/rfc/rfc2104.txt) rules. Here we use the Java Base64 encoding method.

    ```
    Signature = Base64( HMAC-SHA1( AccessSecret, UTF-8-Encoding-Of(StringToSign) ) )
    ```

    **Note:** RFC2104 when calculating signatures `AccessKeySecret` followed by the ampersand \(`&`\), and the hexadecimal ASCII value of an ampersand is 38.

3.  Encode the value of `Signature` according to the [RFC3986](http://tools.ietf.org/html/rfc3986) rules to the canonicalized query string URL.

## Sample 1. Parameter Concatenation Method {#section_rzy_tyb_wdb .section}

Take calling [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) as an example. You have the AccessKeyID=testid and AccessKeySecret=testsecret created in the console.

1.  Create a canonicalized query string.

    ```
    
    http://ecs.aliyuncs.com/?Timestamp=2016-02-23T12:46:24Z&Format=XML&AccessKeyId=testid&Action=DescribeRegions&SignatureMethod=HMAC-SHA1&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf&Version=2014-05-26&SignatureVersion=1.0
    ```

2.  Create a variable [`StringToSign`](#StringToSign) to be calculated by using the canonicalized query string.

    ```
    GET&%2F&AccessKeyId%3Dtestid%26Action%3DDescribeRegions%26Format%3DXML%26SignatureMethod%3DHMAC-SHA1%26SignatureNonce%3D3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf%26SignatureVersion%3D1.0%26Timestamp%3D2016-02-23T12%253A46%253A24Z%26Version%3D2014-05-26
    ```

3.  Calculate the HMAC-SHA1 value. Because you have the AccessKeySecret=testsecret, the Key used in the RFC2104 rules is `testsecret&`, and the HMAC-SHA1 value is `OLeaidS1JvxuMvnyHOwuJ+uX5qY=`. Here we use the Java Base64 encoding method.

    ```
    Signature = Base64( HMAC-SHA1( AccessSecret, UTF-8-Encoding-Of(StringToSign) ) )
    ```

4.  Encode the value of Signature according to the [RFC3986](http://tools.ietf.org/html/rfc3986) rules and add `Signature=OLeaidS1JvxuMvnyHOwuJ%2BuX5qY%3D` to the URL in [Step 1](#Step1).

    ```
    http://ecs.aliyuncs.com/?SignatureVersion=1.0&Action=DescribeRegions&Format=XML&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf&Version=2014-05-26&AccessKeyId=testid&Signature=OLeaidS1JvxuMvnyHOwuJ%2BuX5qY%3D&SignatureMethod=HMAC-SHA1&Timestamp=2016-02-23T12%253A46%253A24Z
    ```


Now you can use a Web browser, curl, wget or other tools to send HTTP request for calling `DescribeRegions` and view the Alibaba Cloud region list.

## Sample 2. Programming Language Method {#section_xzy_tyb_wdb .section}

Assume that you are calling the [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) to describe the Alibaba Cloud region list. You have the AccessKeyID=testid and AccessKeySecret=testsecret created in the console, and all request parameters are stored in a Java `Map<String, String>` object.

1.  Predefined encoding methods.

    ```
    
    private static final String ENCODING = "UTF-8";
    private static String percentEncode(String value) throws UnsupportedEncodingException {
      return value ! = null ? URLEncoder.encode(value, ENCODING).replace("+", "%20").replace("*", "%2A").replace("%7E", "~") : null;
    }
    ```

2.  Predefine the format of the parameter `Timestamp`. The parameter `Timestamp` must conform to the [ISO8601](intl.en-US/API Reference/Appendix/ISO 8601 Time Format.md#), and use the offset from Coordinated Universal Time \(UTC\) for the date time.

    ```
    
    private static final String ISO8601_DATE_FORMAT = "yyyy-MM-dd'T'HH:mm:ss'Z'";
    private static String formatIso8601Date(Date date) {
      SimpleDateFormat df = new SimpleDateFormat(ISO8601_DATE_FORMAT);
      df.setTimeZone(new SimpleTimeZone(0, "GMT"));
      return df.format(date);
    }
    ```

3.  Construct a request string.

    ```
    
    final String HTTP_METHOD = "GET";
    Map parameters = new HashMap();
    // Add request parameters
    parameters.put("Action", "DescribeRegions");
    parameters.put("Version", "2014-05-26");
    parameters.put("AccessKeyId", "testid");
    parameters.put("Timestamp", formatIso8601Date(new Date()));
    parameters.put("SignatureMethod", "HMAC-SHA1");
    parameters.put("SignatureVersion", "1.0");
    parameters.put("SignatureNonce", UUID.randomUUID().toString());
    parameters.put("Format", "XML");
    // Sort the parameters
    String[] sortedKeys = parameters.keySet().toArray(new String[]{});
    Arrays.sort(sortedKeys);
    final String SEPARATOR = "&";
    // Create the variable stringToSign
    StringBuilder stringToSign = new StringBuilder();
    stringToSign.append(HTTP_METHOD).append(SEPARATOR);
    stringToSign.append(percentEncode("/")).append(SEPARATOR);
    StringBuilder canonicalizedQueryString = new StringBuilder();
    for(String key : sortedKeys) {
    // Encode the key and its value
      canonicalizedQueryString.append("&")
      .append(percentEncode(key)).append("=")
      .append(percentEncode(parameters.get(key)));
    }
    // Encode the variable canonicalizedQueryString
    stringToSign.append(percentEncode(
      canonicalizedQueryString.toString().substring(1)));
    ```

4.  Sign and encode the signature. Because you have the AccessKeySecret=testsecret, the Key for computing HMAC is `testsecret&` and the value of signature after calculation is `OLeaidS1JvxuMvnyHOwuJ%2BuX5qY%3D`.

    ```
    
    // A sample code for calculating the signature
    final String ALGORITHM = "HmacSHA1";
    final String ENCODING = "UTF-8";
    key = "testsecret&";
    Mac mac = Mac.getInstance(ALGORITHM);
    mac.init(new SecretKeySpec(key.getBytes(ENCODING), ALGORITHM));
    byte[] signData = mac.doFinal(stringToSign.getBytes(ENCODING));
    String signature = new String(Base64.encodeBase64(signData));
    ```

    After adding the Signature parameter, the request URL encoded according to [RFC3986](http://tools.ietf.org/html/rfc3986) rules is ready to use.

    ```
    http://ecs.aliyuncs.com/?SignatureVersion=1.0&Action=DescribeRegions&Format=XML&SignatureNonce=3ee8c1b8-83d3-44af-a94f-4e0ad82fd6cf&Version=2014-05-26&AccessKeyId=testid&Signature=OLeaidS1JvxuMvnyHOwuJ%2BuX5qY%3D&SignatureMethod=HMAC-SHA1&Timestamp=2016-02-23T12%253A46%253A24Z
    ```

5.  Use a Web browser, curl, wget or other tools to send HTTP Request.

    ```
    <DescribeRegionsResponse>
     <Regions>
         <Region>
             <LocalName>Qingdao</LocalName>
             <RegionId>cn-qingdao</RegionId>
         </Region>
         <Region>
             <LocalName>Hangzhou</LocalName>
             <RegionId>cn-hangzhou</RegionId>
         </Region>
     </Regions>
     <RequestId>833C6B2C-E309-45D4-A5C3-03A7A7A48ACF</RequestId>
    </DescribeRegionsResponse>
    ```


By parsing this XML schema output, you can obtain the region and region ID list of Alibaba Cloud. If you set the `Format=JSON`, the response results are in JSON format. For more information, see [Response results](intl.en-US/API Reference/Call methods/Response results.md#).

