# Know Your Request Object


## HTTPServletRequest
The `HServletRequestttp` interface is an extension of `ServletRequest` that provides additional HTTP protocol-specific information about a received request.
It specifies dozens of methods that you can use to obtain details about an HTTP request. It also permits you to set request attributes (different from request parameters).


### Request Param
Request parameters come in two different forms:

  1. Query parameters (also called URI parameters)
  2. An application/x-www-form-urlencoded or multipart/form-data encoded request body(typically called post variables or form variables).

#### ➤ Query Parameters

Query parameters are supported with all request methods and are contained in the first line of data in an HTTP request
_**Example:**_

    GET /index.jsp?productId=9854521&category=Book HTTP/1.1

In the above example there are two query parameters one is `productId` and another one is the category.
#### ➤ POST Variables
If we want to pass the same parameters in the request body as post variables
_**Example: **_

    POST /index.jsp?returnTo=productPage HTTP/1.1
    HSOT: www.example.com
    Content-Length: 48
    Contest-Type: application/x-www-form-urlencoded

    addToCart&productId=9854521&category=Book

This post request has post variables and query parameter both.

The Servlet API does not differentiate between the two types of parameters.
If we call the parameter-related methods on a request object returns parameters whether they were delivered as query parameters or post variables.


### Get Params
  * The `getParameter` method returns a single value for a parameter. If the parameter has multiple values, it returns the first value

  * The `getParameterValues` returns an array of values for a parameter.

  * The `getParameterMap` method returns a `java.util.Map<String, String[]>` containing all the parameter names mapped to their values

  * The `getParameterNames` method returns an enumeration of the names of all the available parameters

##### ➤➤ Note To Remember
When we call `getParameter`, `getParameterValues`, `getParameterMap` or `getParameterNames` for the first time on a request object, the web container determines whether the request contains post variables by obtaining the request's `InputStream`.
Remember that the Request's `InputStream` can be read only once. If you call `getInputStream` or `getReader` request containing post variables and then later attempt to retrieve parameters in that request, the attempt to retrieve the parameters results in an `IllegalStateException`.
Likewise, if you retrieve parameters on a request containing post variables and then later call `getInputStream` or `getReader`, IT will fail with an `IllegalStateException`.

### Know Request Content
There are several methods that come in handy when you need help determine the type, length, and encoding of the content of the HTTP request.

  * The `getContentType` method returns the MIME content type of the request such as_ application/x-www-form-urlencoded_ , _application/json_ , _text/plain_.

  * The `getContentLength`  method both return the number of bytes in the request body(the content length).

  * The `getContentLengthLong`(Minimum servlet 3.1 specification in Java EE 7) method being useful for requests whose content might exceed gigabytes.

  * The `getCharacterEncoding` method returns the character encoding (such as _UTF-8_ or _ISO-8859-1_) of the request contents whenever the request contains character-type content.

### Know Request Characteristics
  * The `getRequestURL`: Returns the entire URL that the client used to make the request, including protocol( HTTP or HTTPS ), server name, port number, and server path but not including the
query string.
So, in a request to _http://www.example.org/application/index.jsp?category=Books_
`getRequestURL` returns _http://www.example.org/application/index.jsp_

  * The `getRequestURI`: This is slightly different from `getRequestURL` in that it returns only the server path part of the URL.
As previous example, that would be _/application/index.jsp_

  * The `getServletPath`: Similar to `getRequestURI`, this returns even less of the URL.
If the request is _/hello-world/greeting? foo=world_, the application is deployed as _/hello-world_ on Tomcat, and the servlet-mappings are _/greeting_, _/hello_, and _/thank_, `getServletPath` returns only the part of the URL used to match the servlet mapping:_ /greeting._

  * The `getHeader`: Returns the value of a header with the given name. The case of the header does not have to match the case of the string passed into the method, so `getHeader`( " content-type " ) can match the Content-Type header. If there are multiple headers with the same name, this returns only the first value. In such cases, you would want to use the `getHeaders` method to return an enumeration of all the values.

  * The `getHeaderNames`: Returns an enumeration of the names of all the headers in the request. A great way to iterate over the available headers.

  * The `getIntHeader`: If you have a particular header that you know is always a number, you can call this to return the value already converted to a number. It throws a `NumberFormatException` if the header cannot be converted to an integer.

  * The `getDateHeader`: You can call this to return the (millisecond) Unix timestamp-equivalent of a header value that represents a valid timestamp. It throws an `IllegalArgumentException` if the header value is not recognized as a date.

