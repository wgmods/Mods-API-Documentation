Module **web** allows you to work with web resources.

## Available methods:

- [getAllowedUrls()](#getAllowedUrls)
- [addAllowedUrl(encodedUrl)](#addAllowedUrlencodedUrl)
- [openUrl(url)](#openUrlurl)
- [urlEncode(query)](#urlEncodequery)
- [urlQuote(s, safe='/')](#urlQuotes-safe)

---

### getAllowedUrls()
This function returns a list, a list of allowed URLs.

#### Returns
- list

---

### addAllowedUrl(encodedUrl)
This function adds a special encoded URL to the list of allowed URLs. You can request a special encoded URL from support.

#### Input parameters
- encodedUrl - a special encoded URL

---

### openUrl(url)
The method is similar to **urllib2.urlopen(url, data=None)**.

It allows you to open a URL from the list of allowed URLs.

You can see full documentation on this function on the official Python website here: https://docs.python.org/2/library/urllib2.html#urllib2.urlopen

#### Input parameters
- url - an allowed URL, str

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
