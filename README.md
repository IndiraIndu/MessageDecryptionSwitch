# Message Layer Encryption Bypass

Introduction:
Now a days it has become a compulsory requirement to have message layer encrypted in all
applications. PCI Council has strict rules for data transmission and insists on enforcing strong
secure transport protocols, use of trusted keys/certificates and strong layers encryption and
message layer encryption further enhances security for data on transit. Especially in banking
and other applications that handle sensitive user data, HTTP message body encryption is
implemented as extra layer of security in addition to two way ssl. This way even if an adversary
eavesdropping is able to strip down SSL layer, he/she will still be left with encrypted message
content without means to decrypt it. The extender we developed comes in handy for a pentester
in removing this encryption layer and helps pentester in exploiting the application.

Current limitations with Burp:
● BurpSuite cannot distinguish if a HTTP Message body is encrypted or not.
● This impacts the capability of Active scanner in identifying vulnerabilities.
● Does not have an feature to bypass message layer encryption.
So we developed a burp extender that helps bypassing this message layer security. Our burp
extender identifies if the incoming HTTP message body is encrypted and bypasses this
encryption. This is very much helpful for pentesters in carrying out dynamic & manual
assessment for these applications. The following is the workflow.

Workflow:
● User can load and save message encryption certificates in PKCS12 format for different
hosts.
● Incoming messages are filtered based on host name of chosen certificate.
● The filtered messages are now differentiated if they are encrypted or not. Unencrypted
messages are directly sent to scanner(request)/user(response).
● Encrypted messages are parsed to extract the encrypted body content from HTTP
Request/Response.
● Based on the chosen certificate, incoming HTTP message body is encrypted/decrypted
as required.
● Encrypted request body parameters are decrypted and sent to Scanner for payload
injection.
● Injected requests are now again encrypted before sending to server.
● Received encrypted response body parameters are decrypted before sending to scanner
or shown to user.
