# What? #

WebFinger, aka [Personal Web Discovery](http://www.abstractioneer.org/2009/04/personal-web-discovery.html).

i.e. **We're bringing back the finger protocol, but using HTTP this time.**

# Background #

Back in the day you could, given somebody's UNIX account (email address), type `finger email@example.com` and get some information about that person, whatever they wanted to share:  perhaps their office location, phone number, URL, current activities, etc.

The finger protocol, sadly, died.

Fast-forward to Web 2.0.  We're currently bickering about how we do interop between all these social web services, and even how we represent a person's identity.  The two main identity identifier camps are email addresses and URLs.

Let's review the pros and cons of both:

| | Email address | URL |
|:|:--------------|:----|
| People associate it with... | a person      | usually a thing, place, or document; _sometimes_ a person |
| Is readable? | -             | X   |
| Is writeable? | X             | X   |

People have been trying to use URLs as identifiers for people (as OpenID does), as it has great readability/discoverability properties, but this effort has largely failed because of UI/UX design failings, user confusion about URLs, etc.

It's now increasingly accepted that email addresses would be good identifiers for people (since that's what people are used to already, and have on business cards and in their addressbooks, etc.), but we're back to the original problem that email addresses are write-only.

If I give you my email address today, you can't do anything with it except email me.  I can't attach public metadata to my email address to give you more information.

WebFinger is about making email addresses more valuable, by letting people attach public metadata to them.  That metadata might include:

  * public profile data
  * pointer to identity provider (e.g. OpenID server)
  * a public key
  * other services used by that email address (e.g. Flickr, Picasa, Smugmug, Twitter, Facebook, and usernames for each)
  * a URL to an avatar
  * profile data (nickname, full name, etc)
  * whether the email address is also a JID, or explicitly declare that it's NOT an email, and ONLY a JID, or any combination to disambiguate all the addresses that look like something@somewhere.com
  * or even a public declaration that the email address **doesn't have public metadata**, but has a pointer to an endpoint that, provided authentication, will tell you some protected metadata, depending on who you authenticate as.

... but rather than fight about the exact contents of that file, WebFinger is about making that file discoverable _at all_.  The community can explore and innovate within that discovery file later.

