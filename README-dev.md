# Stonefish License Manager — Developer Information

The Stonefish License Manager (SLiM) contains a powerful command-line tool and
Python library designed to efficiently manage software licenses. This document
provides comprehensive information on utilizing SLiM with various license
sources and integration steps for your Python software.

For other Stonefish product (e.g., [Stonefish Code
Shield](https://github.com/stonefish-dev/code-shield)), see
[here](https://github.com/stonefish-dev/).

SLiM supports licenses from multiple sources, including:

- [Stonefish License Creator](https://github.com/stonefish-dev/license-creator)
- [Keygen](https://keygen.sh/)
- [LicenseSpring](https://licensespring.com/)
- [Cryptolens](https://cryptolens.io/)

Note that using a service other than Stonefish may incur additional fees from
the chosen service.

### Installation

Ensure that you have Python 3.8 or a later version installed on your system.
To (un)install SLiM, execute the following command:

<!--pytest.mark.skip-->

```bash
pip [un]install stonefish-license-manager
```

### Getting Started with SLiM

Follow these steps to integrate SLiM into your Python software:

1. Provide users with a license obtained from one of the supported sources.

2. Instruct users to install the license using the command

   ```
   slim install <license-file-or-key>
   ```

3. Include a license check within your software. See the code snippet below for
   implementation details.

4. Optionally, safeguard your software through obfuscation techniques, such as
   those provided by
   [Stonefish Code Shield](https://github.com/stonefish-dev/code-shield), to
   prevent unauthorized tampering with the license check.

### Stonefish License Creator (SLiC)

The Stonefish License Creator (SLiC) generates cryptographic offline licenses
that are compatible with SLiM. These licenses can have specific expiry times
and can be limited to certain machines. For detailed instructions on utilizing
SLiC, refer to the [SLiC
documentation](https://github.com/stonefish-dev/license-creator).

Implement the license check in your software with the following Python code:

<!--pytest.mark.skip-->

```python
import sys

import stonefish_license_manager as slim

# The following Python code performs a license check using SLiM.
# It raises a slim.LicenseError if no valid license is found.
try:
    license = slim.slic.find_license_and_validate(
        "your-vendor-id",  # Vendor ID assigned by Stonefish
        "your-product-id",  # Unique product ID (e.g., a random UUIDv4)
        # optional: env or global variable names that may contain a key
        # variable_names=["FOO_KEY", "BAR_KEY"],
    )
except slim.LicenseError as e:
    e.show()
    sys.exit(1)

# The license object contains useful information for further processing.
print(license.data)
```

```python
{
    'vendor': {'id': '6697c7f2-ad29-42c6-8b78-8ddb2a56bc0b'},
    'product': {
        'id': '83da0a2b-751b-4a3d-9c4f-3eaf00541d9d',
        'name': 'SLiC demo'
    },
    'user': {
        'id': '869eaad6-ff94-47a9-ae4c-00315e9a11b9',
        'name': 'J. Doe',
        'email': 'j.doe@example.com'
    },
    'license': {
        'expiry': '2030-01-01T00:00:00Z',
        'id': 'bfc81d86-72d3-4359-ac17-9ca316828165',
        'created': '2024-01-09T13:05:01Z'
    }
}
```

To test the functionality, try the following SLiC demo licenses:

```
slicv1/eyJ2ZW5kb3IiOnsiaWQiOiI2Njk3YzdmMi1hZDI5LTQyYzYtOGI3OC04ZGRiMmE1NmJjMGIifSwicHJvZHVjdCI6eyJpZCI6IjgzZGEwYTJiLTc1MWItNGEzZC05YzRmLTNlYWYwMDU0MWQ5ZCIsIm5hbWUiOiJTTGlDIGRlbW8ifSwidXNlciI6eyJpZCI6Ijg2OWVhYWQ2LWZmOTQtNDdhOS1hZTRjLTAwMzE1ZTlhMTFiOSIsIm5hbWUiOiJKLiBEb2UiLCJlbWFpbCI6ImouZG9lQGV4YW1wbGUuY29tIn0sImxpY2Vuc2UiOnsiZXhwaXJ5IjoiMjAzMC0wMS0wMVQwMDowMDowMFoiLCJpZCI6ImJmYzgxZDg2LTcyZDMtNDM1OS1hYzE3LTljYTMxNjgyODE2NSIsImNyZWF0ZWQiOiIyMDI0LTAxLTA5VDEzOjA1OjAxWiJ9fQ==.5bOe83O_KhoahbWw6Z-06kY6vHHjA0EbsbVidqmloerqKo2YBZJ3fN2-zevlSkvJtY12iZJv51BR3kbTd8hsBQ==
```

(valid) and

```
slicv1/eyJ2ZW5kb3IiOnsiaWQiOiI2Njk3YzdmMi1hZDI5LTQyYzYtOGI3OC04ZGRiMmE1NmJjMGIifSwicHJvZHVjdCI6eyJpZCI6IjgzZGEwYTJiLTc1MWItNGEzZC05YzRmLTNlYWYwMDU0MWQ5ZCIsIm5hbWUiOiJTTGlDIGRlbW8ifSwidXNlciI6eyJpZCI6Ijg2OWVhYWQ2LWZmOTQtNDdhOS1hZTRjLTAwMzE1ZTlhMTFiOSIsIm5hbWUiOiJKLiBEb2UiLCJlbWFpbCI6ImouZG9lQGV4YW1wbGUuY29tIn0sImxpY2Vuc2UiOnsiZXhwaXJ5IjoiMjAyNC0wMS0wOVQxMzoyMDoyNloiLCJpZCI6Ijk3NWQ4YzRkLTIyNTQtNGMzYi1hYWNhLWFiYTY5ZWVhZTM2NyIsImNyZWF0ZWQiOiIyMDI0LTAxLTA5VDEzOjIwOjI1WiJ9fQ==.ISsP_ZMfQWnvpUMOkEMlr6da7hXSZOfuny3SxTA7eAoYlaHijbP9ntHzqSusQK08HRr16WCD8FHSGw3pFmxKDQ==
```

(expired).

<!--prai:split-->

### Keygen

[Keygen](https://keygen.sh/) is an online service that provides comprehensive
software license management solutions. It offers various schemes to manage
licenses, including online and offline licenses, license pools, maximum usage
limits, machine and process constraints, automatic expiry, and more. These
schemes are fully supported by SLiM.

For the best experience with SLiM, we recommend providing license check-out
files (`.lic`) to your users, as this allows for efficient offline license
verification.

Please refer to the code snippet below to integrate Keygen into your software
application:

<!--pytest.mark.skip-->

```python
import stonefish_license_manager as slim

# Raises slim.LicenseError if no valid license is found:
license, meta = slim.keygen.find_license_and_validate(
    "your-keygen-account-id",
    "your-keygen-product-id",
    # optional: env or global variable names that may contain a key
    # variable_names = ["FOO_KEY", "BAR_KEY"],
    # optional: Cache control
    # cache_control = f"max-age={3 * 24 * 3600},max-stale={4 * 24 * 3600}",
)

# The license object contains useful information for further processing.
print(license.data)
print(meta)
```

```python
{
    'id': '0158a4cd-c913-4e8e-9d01-57fb637d649d',
    'type': 'licenses',
    'attributes': {
        'name': 'Valid Demo License',
        'key': 'DEMO-AABCCD-7F6E4A-E64012-340C88-V3',
        'expiry': '2024-01-29T03:24:25.013Z',
        'status': 'ACTIVE',
        'uses': 0,
        'suspended': False,
        'scheme': None,
        'encrypted': False,
        'strict': False,
        'floating': True,
        'protected': True,
        'version': None,
        'maxMachines': 10,
        'maxProcesses': None,
        'maxCores': None,
        'maxUses': None,
        'requireHeartbeat': False,
        'requireCheckIn': False,
        'lastValidated': '2024-01-04T14:04:52.724Z',
        'lastCheckIn': None,
        'nextCheckIn': None,
        'lastCheckOut': None,
        'metadata': {'token': 'activ-bdf04c15b9d77b7dc4d56a91a0f45982v3'},
        'created': '2021-04-20T18:28:43.582Z',
        'updated': '2024-01-04T14:04:52.732Z'
    },
    'relationships': {
        'account': {
            'links': {
                'related': '/v1/accounts/1fddcec8-8dd3-4d8d-9b16-215cac0f9b52'
            },
            'data': {
                'type': 'accounts',
                'id': '1fddcec8-8dd3-4d8d-9b16-215cac0f9b52'
            }
        },
        # [...]
    }
}
{
    'ts': '2024-01-04T14:04:52.737Z',
    'valid': True,
    'detail': 'is valid',
    'code': 'VALID'
}
```

> [!TIP]
>
> Keygen API responses don't contain all information you might want to provide
> to your software or your users. You can explicitly add any data to the
> `data["attributes"]["metadata"]` field though. Metadata entries that are
> automatically processed by SLiM are
>
> - `token` (for token authorization, see
>   [here](https://keygen.sh/docs/api/licenses/#licenses-relationships-activation-tokens))
> - `productName` (the corresponding product name)
> - `email` (the user email address)

### LicenseSpring

[LicenseSpring](https://licensespring.com/) is an online service that offers
advanced software license management and sales capabilities.

For Stonefish, we strongly advise providing _license refresh files_ to your
users. These files enable efficient license verification and maintenance.

Please refer to the code snippet below to integrate LicenseSpring into your
software application:

<!--pytest.mark.skip-->

```python
import stonefish_license_manager as slim

# Raises slim.LicenseError if no valid license is found:
license = slim.license_spring.find_license_and_validate(
    "your-ls-product-code",
    "your-ls-shared-key",
    "your-ls-api-key",
    # optional: env or global variable names that may contain a key
    # variable_names = ["FOO_KEY", "BAR_KEY"],
    # optional: Cache control
    # cache_control = f"max-age={3 * 24 * 3600},max-stale={4 * 24 * 3600}",
)

# The `license` object contains useful information for further processing.
print(license.data)
```

```python
{
    'id': 1696713670593549,
    'order_store_id': 'ca16501a20ef4a7b9a0cf28cb42f0b16',
    'license_active': True,
    'license_enabled': True,
    'license_type': 'time-limited',
    'license_key': 'K59J-QG4B-AM3J-XVSZ',
    'is_trial': False,
    'validity_period': '2024-10-07T00:00:00.000Z',
    # ...
}
```

### Cryptolens

[Cryptolens](https://cryptolens.io/) is an online service that specializes in
software license management and sales.

Please refer to the code snippet below to integrate Cryptolens into your
software application:

<!--pytest.mark.skip-->

```python
import stonefish_license_manager as slim

# Raises slim.LicenseError if no valid license is found:
license = slim.cryptolens.find_license_and_validate(
    981653164,  # your product ID
    "your-token",
    # optional: env or global variable names that may contain a key
    # variable_names = ["FOO_KEY", "BAR_KEY"],
    # optional: Cache control
    # cache_control = f"max-age={3 * 24 * 3600},max-stale={4 * 24 * 3600}",
)

# The license object contains useful information for further processing.
print(license.data)
```

```python
{
    'id': 1696713670593549,
    'order_store_id': 'ca16501a20ef4a7b9a0cf28cb42f0b16',
    'license_active': True,
    'license_enabled': True,
    'license_type': 'time-limited',
    'license_key': 'K59J-QG4B-AM3J-XVSZ',
    'is_trial': False,
    'validity_period': '2024-10-07T00:00:00.000Z',
    # ...
}
```

### Additional Information

For more information, please reach out to support@mondaytech.com.
