Module **web** allows you to work with web resources.

## Available methods:

- [getAllowedUrls()](#getAllowedUrls)
- [addAllowedUrl(encodedUrl)](#addAllowedUrlencodedUrl)
- [openUrl(urlurl, data=None)](#openUrlurlurl-dataNone)
- [urlEncode(query)](#urlEncodequery)
- [urlQuote(s, safe='/')](#urlQuotes-safe)
- [fetchURL(url, callback, headers, timeout, method)](#fetchURLurl-callback-headers-timeout-method)

---

### getAllowedUrls()
This function returns a list, a list of allowed URLs.

#### Returns
- list

---

### addAllowedUrl(encodedUrl)
This function adds a special encoded URL to the list of allowed URLs. You can request a special encoded URL from support.
Returns true if url successfully added, and false instead.

#### Input parameters
- encodedUrl - a special encoded URL

#### Returns
- bool

---

### openUrl(urlurl, data=None)
The method is similar to **urllib2.urlopen(url, data=None)**.

It allows you to open a URL from the list of allowed URLs.

You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/urllib2.html#urllib2.urlopen

#### Input parameters
- url - an allowed URL with request, str
- data - data for publishing on server, if needed, str

---

### urlEncode(query)
The method is similar to **urllib.urlencode(query, doseq=0)**. 

It is used for coding a line in the format following the rules for data in queries.

You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/urllib.html#urllib.urlencode

---

### urlQuote(s, safe='/')
The method is similar to **urllib.quote(string, safe)**.
It replaces all special symbols by strings **%nn**. Numbers, Latin characters and underscore characters, dots and hyphens are not coded. Spaces are converted into the string **%20**.

You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/urllib.html#urllib.quote

#### Input parameters
- s - the line where replacements are made, str
- safe - is a symbols that cannot be converted

---

### fetchURL(url, callback, headers, timeout, method)
Execute async web request, response will return in callback parameter.

It correct works with both http and https URLs.


#### Input parameters
- url - URL with data, str
- callback - callback witch will receive response, function
- headers - headers, str
- timeout - timeout, int
- method - request method, str

#### Example:
    def callback(response):
        utils.logInfo('{}'.format(response))

    web.fetchURL(url_with_data, callback, '', 5, 'GET')
    
---
