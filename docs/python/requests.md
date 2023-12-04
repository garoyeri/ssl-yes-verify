---
sidebar_position: 1
tags: [linux, python]
---

# Python Requests Library

Modern Python applications *should* be using [Certifi](https://pypi.org/project/certifi/) and [Requests](https://docs.python-requests.org/en/latest/index.html) for their HTTP client needs. Certifi ships its own certificate authority (CA) bundle that is updated along with the application, but you can override it in the Requests library by passing an environment variable to the process.

According to the documentation: [Advanced Usage - Requests](https://docs.python-requests.org/en/latest/user/advanced/#ssl-cert-verification), there are two variables you can use:

1. `REQUESTS_CA_BUNDLE`
2. `CURL_CA_BUNDLE`

These can be set to a file: `/etc/ssl/certs/ca-certificates.crt` or a directory (that's already been processed using your OS tool `update-ca-trust` or `update-ca-certificates`).

## Beware of urllib

Some older libraries may still be using [urllib3](https://urllib3.readthedocs.io/en/stable/index.html). While this does support using Certifi: [User Guide urllib3](https://urllib3.readthedocs.io/en/stable/user-guide.html#certificate-verification), it doesn't have a runtime override unless you make one yourself. Looking at the sample code in the documentation site:

```python
# Source: https://urllib3.readthedocs.io/en/stable/user-guide.html#certificate-verification
import certifi
import urllib3

http = urllib3.PoolManager(
    cert_reqs="CERT_REQUIRED",
    ca_certs=certifi.where()
)
```

The `PoolManager` takes the Certifi certificate authority list. You would need to add your own logic here to allow a runtime override of the certificate list. (If someone has a working code sample of this they are willing to contribute, please make a PR).
