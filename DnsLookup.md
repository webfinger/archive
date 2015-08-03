# Introduction #

We need to figure out the best way to use DNS to do the initial discovery of the domain's XRD file, given the domain name.

SRV records provide for a hostname and port, but no path component.

TXT records are the favorite catch-all, but it's not strictly what TXT records are for.

A TXT record for discovery on `example.com` might look like:

```
example.com.   300  IN  TXT  "v=xrd1 url=http://meta.example.com/site/my-xrd.xml"
```