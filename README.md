# cs50-pset6
Implements the functionality of a web server written in C.
The functions I worked on were:

lookup

Returns the following:
text/css for any file whose path ends in .css (or any capitalization thereof),

text/html for any file whose path ends in .html (or any capitalization thereof),

image/gif for any file whose path ends in .gif (or any capitalization thereof),

image/x-icon for any file whose path ends in .ico (or any capitalization thereof),

image/jpeg (not image/jpg) for any file whose path ends in .jpg (or any capitalization thereof),

text/javascript for any file whose path ends in .js (or any capitalization thereof),

text/x-php for any file whose path ends in .php (or any capitalization thereof), or

image/png for any file whose path ends in .png (or any capitalization thereof), or

NULL otherwise.

parse
Function parses (i.e., iterates over) line, extracting its absolute-path and query and storing them at abs_path and query, respectively.

Request-line: method SP request-target SP HTTP-version CRLF
wherein SP represents a single space ( ) and CRLF represents \r\n. None of method, request-target, and HTTP-version, meanwhile, may contain SP.

request-target: absolute-path [ "?" query ]
whereby absolute-path (which will not contain ?) must start with / and might optionally be followed by a ? followed by a query, which may not contain ".

If request-line is not consistent with these rules, respond to the browser with 400 Bad Request and return false.

Even if request-line is consistent with these rules,

if method is not GET, respond to the browser with 405 Method Not Allowed and return false;

if request-target does not begin with /, respond to the browser with 501 Not Implemented and return false;

if request-target contains a ", respond to the browser with 400 Bad Request and return false;

if HTTP-version is not HTTP/1.1, respond to the browser with 505 HTTP Version Not Supported and return false; or

query
Store at the address in query the query substring from request-target. If that substring is absent (even if a ? is present), then query should be "", thereby consuming one byte, whereby query[0] is '\0'. You may assume that the memory to which query points will be at least of length LimitRequestLine + 1.
For instance, if request-target is /hello.php or /hello.php?, then query should have a value of "". And if request-target is /hello.php?q=Alice, then query should have a value of q=Alice.

load
Complete the implementation of load in such a way that the function:
reads all available bytes from file,
stores those bytes contiguously in dynamically allocated memory on the heap,
stores the address of the first of those bytes in *content, and
stores the number of bytes in *length.

indexes

The function, given a /path/to/a/directory, returns /path/to/a/directory/index.php if index.php actually exists therein, or /path/to/a/directory/index.html if index.html actually exists therein, or NULL. In the first of those cases, the function dynamically allocate memory on the heap for the returned string.
