#summary the WebFinger protocol
#labels Featured

# WARNING: DRAFT #

This is a draft, with updates based on various messages and blog posts along with various specs as they have matured over the past six months.

# Protocol #

The goal of the protocol is to get an [XRD](XrdFiles.md) XML file describing how to find a user's public metadata from that user's
email address or email address like identifier.  The following describes the steps in the Webfinger protocol specifically,
and ignores the options in the underlying protocols that don't apply (mostly the Link: header).
The [Requirements](Requirements.md) page gives some background on the requirements that went into
the design of the WebFinger protocol.

## Normalize and parse the email address ##

Given an email address, **foo@example.com**, turn it into a URI by prepending "acct:" if necessary.  This lets machines digest it more easily.
Grab the host of **acct:foo@example.com** -- in this case, example.com.

## Get the domain's host-meta XRD file ##

First, you need to get the host's host-meta XRD file.  In this case, example.com's.  This is available at
`https://example.com/.well-known/host-meta`.  If there's no response to an SSL connection there,
try `http://example.com/.well-known/host-meta`.  Follow 3xx redirects; remember if anything _wasn't_ retrieved via SSL
connections with valid certificates.

Note that this needs to be done only the first time for each host-meta, after that you can cache the results using standard
HTTP caching semantics.

### Retrieving host-meta ###

```
GET /.well-known/host-meta HTTP/1.1
Host: example.com
```

The world has enough well-known URLs (`/favicon.ico`, `/crossdomain.xml`, `/robots.txt`), and we felt dirty adding another, so
the `/.well-known/` prefix (see [draft-hammer-hostmeta-05](http://tools.ietf.org/html/draft-hammer-hostmeta-05)) is the
virtual directory where we hope future specs add their well-known URLs too.

## Verify the host-meta XRD file's signature ##

If the host-meta file wasn't retrieved via SSL, check for an XRD signature.

If it's not signed and either it's ever been signed on prior retrievals, or it's a big company's site which you expect to use
proper security, be afraid.  Abort the process.  Probably MITM.  You can fall back to manual discovery (asking the user for info).

Also, once you verify the signature, double check that the XRD _Host_ element matches your host name - e.g., example.com.
This keeps example.com from stealing someone else's host-meta file and passing it off as their own.

## Look for the XRD "lrdd" Link ##

Look for the Link element with rel="lrdd" and attribute _template_ in the domain XRD file.
Grab the value of the template attribute.  This is a template to map from your acct: URI to the location
of its metadata.

e.g.

```
<Link rel="lrdd" template="https://meta.example.org/?q={uri}"  type="application/xrd+xml" />
```

So given {uri} = acct:foo@example.com, this yields after swizzling:

```
https://meta.example.org/?q=acct%3Afoo%40example.com
```

(See [draft-hammer-hostmeta-05](http://tools.ietf.org/html/draft-hammer-hostmeta-05#section-3.2.1))

## Get user's XRD file ##

```
GET /?q=acct%3Afoo%40example.com HTTP/1.1
Host: meta.example.org
```

Follow 3xx etc. as normal.  Again, if the SSL cert doesn't check out or if this isn't an https URL,
remember secure=false.  Also, verify that the XRD you get in the end has a _Subject_ element that
matches the acct: URI you started with:

```
<Subject>acct:foo@example.com</Subject>
```

Note: Need a big security section describing all the things that need checking.

You'll get back an XRD file containing the _Link_ (s) that you're looking for.  Look for the link(s) with
the rel value you need.  Those are the services you're trying to discover for acct:foo@example.com.

(See [xrd-1.0-wd11](http://www.oasis-open.org/committees/download.php/35678/xrd-1.0-wd11.html#element.link).)

# Appendix #

See also [Eran's implementing-webfinger blog post](http://hueniverse.com/2009/09/implementing-webfinger/).

Respect and use DNS TTLs and HTTP caching/expiry headers.  Also, XRD has an Expires element so honor that.
