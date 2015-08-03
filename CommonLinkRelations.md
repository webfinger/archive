# Relations #

Here is a list of common link relations commonly found in a user's XRD file:

| **Link Relation** | **Source** |
|:------------------|:-----------|
| describedby       | [Link Relation Registry](http://tools.ietf.org/html/draft-nottingham-http-link-header-07#section-6.2.2) |
| http://portablecontacts.net/spec/1.0 | [Portable Contacts](http://portablecontacts.net/draft-spec.html) |
| http://webfinger.net/rel/profile-page | WebFingerProfilePage |
| http://microformats.org/profile/hcard | [hCard](http://microformats.org/profile/hcard) |
| http://gmpg.org/xfn/11 | [XHTML Friends Network](http://gmpg.org/xfn/) |
| http://specs.openid.net/auth/2.0/provider | [Open ID 2.0 Provider](http://openid.net/specs/openid-authentication-2_0.html) |
| http://schemas.google.com/g/2010#updates-from | [Buzz Updates](http://code.google.com/apis/gdata/docs/2.0/basics.html) |

## Example User XRD Document ##

```
<?xml version='1.0'?>
<XRD xmlns='http://docs.oasis-open.org/ns/xri/xrd-1.0'>
	<Subject>acct:joe.gregorio@gmail.com</Subject>
	<Alias>http://www.google.com/profiles/joe.gregorio</Alias>
	<Link rel='http://portablecontacts.net/spec/1.0' 
            href='http://www-opensocial.googleusercontent.com/api/people/'/>
	<Link rel='http://webfinger.net/rel/profile-page' 
            href='http://www.google.com/profiles/joe.gregorio' type='text/html'/>
	<Link rel='http://microformats.org/profile/hcard' 
            href='http://www.google.com/profiles/joe.gregorio' type='text/html'/>
	<Link rel='http://gmpg.org/xfn/11' 
            href='http://www.google.com/profiles/joe.gregorio' type='text/html'/>
	<Link rel='http://specs.openid.net/auth/2.0/provider' 
            href='http://www.google.com/profiles/joe.gregorio'/>
	<Link rel='describedby' 
            href='http://www.google.com/profiles/joe.gregorio' 
            type='text/html'/>
	<Link rel='describedby' 
            href='http://s2.googleusercontent.com/webfinger/?q=acct%3Ajoe.gregorio%40gmail.com&amp;fmt=foaf' 
            type='application/rdf+xml'/>
	<Link rel='http://schemas.google.com/g/2010#updates-from' 
            href='http://buzz.googleapis.com/feeds/118148240205592032989/public/posted' 
            type='application/atom+xml'/>
</XRD>
```