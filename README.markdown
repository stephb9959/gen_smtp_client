Mission
=======

Provide just the SMTP client portion from the SMTP server framework gen_smtp.

The SMTP client supports PLAIN, LOGIN, CRAM-MD5 authentication as well
as STARTTLS and SSL (port 465).

Also included is a MIME encoder/decoder, sort of according to RFC204{5,6,7}.

gen_smtp developers (much thanks to them!):
============================================

+ Andrew Thompson (andrew AT hijacked.us)
+ Jack Danger Canty (code AT jackcanty.com)
+ Micah Warren (micahw AT lordnull.com)

Modifications after split via fork made by:
============================================
+ Bill Barnhill (bill.barnhill AT communitivity.net)

Who is using it?
================

+ Right now the extracted client is only used within the Hermes SMTP server, currently only for testing

If you'd like to share your usage of gen_smtp, please contact me.

Example
==============

Here's an example usage of the client:

<pre>
gen_smtp_client:send({"whatever@test.com", ["andrew@hijacked.us"],
 "Subject: testing\r\nFrom: Andrew Thompson <andrew@hijacked.us>\r\nTo: Some Dude <foo@bar.com>\r\n\r\nThis is the email body"},
  [{relay, "smtp.gmail.com"}, {username, "me@gmail.com"}, {password, "mypassword"}]).
</pre>

The From and To addresses will be wrapped in &lt;&gt;s if they aren't already,
TLS will be auto-negotiated if available (unless you pass `{tls, never}`) and
authentication will by attempted by default since a username/password were
specified (`{auth, never}` overrides this).

If you want to mandate tls or auth, you can pass `{tls, always}` or `{auth,
always}` as one of the options. You can specify an alternate port with `{port,
2525}` (default is 25) or you can indicate that the server is listening for SSL
connections using `{ssl, true}` (port defaults to 465 with this option).

