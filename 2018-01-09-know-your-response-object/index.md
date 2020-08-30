# Know Your Response Object


## HttpServletResponse
The `HttpServletResponse` interface extends `ServletResponse` and provides access to the HTTP protocol-specific properties of a response.<br>
You can use the response object to do things such as

  * Set response headers
  * Write to the response body
  * Redirect the request
  * Set the HTTP status code
  * Send cookies back to the client.

### Writing to Response Body
The most common thing you’ll do with a response object is written content to the response body.

  * This might be HTML to display in a browser
  * An image that the browser is retrieving
  * The contents of a file that the client is downloading.
  * It could be plain text or binary data
  * It might be just a few bytes long or it could be gigabytes long.

The `getOutputStream`: Returns a `javax.servlet.ServletOutputStream`, for sending binary data back, you must use the `ServletOutputStream` to send the response bytes.

The `getWriter`: Returns a `java.io.PrintWriter`, you would probably want to use the `PrintWriter` for returning HTML or some other character-encoded text to the client because this makes it easy to write encoded String s and char s to the response.

Also, you should never use both `getOutputStream` and `getWriter` in the same response. After a call to one, a call to the other will fail with an `IllegalStateException`.<br>
Set the content type or encoding

While you’re writing to the response body, it might be necessary to set the content type or encoding.

`setContentType` and `setCharacterEncoding` methods serves the purpose. You may call these methods as many times as you like; the last call to the method is the one that matters.

#### Note To Remember
  * If you plan to call `setContentType` and `setCharacterEncoding` along with `getWriter`, you must call `setContentType` and `setCharacterEncoding` beforer `getWriter` so that the returned writer is configured for the correct character encoding. Calls made after getWriter are ignored.

  * If you do not call `setContentType` and `setCharacterEncoding` before calling `getWriter`, the returned writer uses the container’s default encoding.

### Setting Headers and Other Response Properties
  * The `setHeader`, `setIntHeader`, and `setDateHeader`: To set nearly any header value you desire.  If the existing response headers already include a header with the name you are setting, the value of that header will be overridden.

  * The `addHeader`, `addIntHeader`, and `addDateHeader`: These versions do not override existing header values, but instead add additional values for the given headers.
  * The `getHeader`, `getHeaders`, `getHeaderNames`, and `containsHeader`: To check which headers have already been set on the response.

  * The `setStatus`: To set the HTTP response status code

  * The `getStatus`: To determine what the current status of the response is

  * The `sendError`: To set the status code, indicate an optional error message to write to the response data, direct the web container to provide an error page to the client, and clear the buffer

  * The `sendRedirect`: To redirect the client to a different URL

