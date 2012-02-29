# Python http-signature

Sign http requests with secure signatures.

## Requirements

* PyCrypto

Optional:

* requests

## Usage

for simple raw signing:

    import http_signature
    
    sig_maker = http_signature.Signer(secret='test.pem', algorithm='rsa-sha256')
    sig_maker.sign('hello world!')

for use with requests:

    import json
    import requests
    from http_signature.requests_auth import HTTPSignatureAuth
    
    auth = HTTPSignatureAuth(key_id='Test', secret='test.pem')
    z = requests.get('https://api.joyentcloud.com/my/packages/Small+1GB', 
                             auth=auth, headers={'X-Api-Version': '~6.5'})

## class initialization parameters:

    http_signature.Signer(secret='', algorithm='rsa-sha256')

`secret`, in the case of an rsa signature, is a path to a private RSA pem file. In the case of an hmac, it is a secret password.  
`algorithm` is one of the six allowed signatures: `rsa-sha1`, `rsa-sha256`, `rsa-sha512`, `hmac-sha1`, `hmac-sha256`, `hmac-sha512`

    http_signature.requests_auth.HTTPSignatureAuth(key_id='', secret='', algorithm='rsa-sha256', headers=None)

`key_id` is the label by which the server system knows your RSA signature or password.  
`headers` is the list of HTTP headers that are concatenated and used as signing objects. By default it is the specification's minimum, the `Date` HTTP header.  
`secret` and `algorithm` are as above.

## License

MIT