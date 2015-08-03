The WebFinger protocol allows looking up meta-data about
a resource. The final protocol has been guided by the
following requirements, which will give some insight
into the design decisions made during development.


## Ease of Install ##
A user with a standard web hosting provider must be
able to use WebFinger. That implies that deploying WebFinger should
be as easy as placing one or two files in a directory.
Since signing of the WebFinger files is needed in some situations,
picking a technology that allows packaging
of signatures and data files together is important,
and thus the choice of XML as a format for XRD, and the
use of XML Signatures.

## Security ##
There must be an ability to sign XRD files. Some
of the resources pointed to via an XRD file, such
as the users OpenID provider, are sensitive and
if corrupted via a Man-in-the-middle attack, or a
defacement attack, could lead users to enter their
usernames and passwords into an untrusted site.
While SSL could solve this problem, it doesn't do
so without conflicting with the 'Ease of Install'
requirement. While signing XRD files for
servers and checking signatures for clients is optional
in the base specifications, there may be follow-on
specifications, or profiles of XRD that require
signatures.
