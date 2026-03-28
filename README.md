# UnitySVC Services - SMTP

This repository hosts SMTP relay service data for the UnitySVC platform.

## Services

### test-mailpit

Test SMTP relay service using Mailpit as upstream. Emails are captured and viewable at [smtp.staging.svcmarket.com](https://smtp.staging.svcmarket.com). No actual delivery occurs.

## Setup

```bash
pip install unitysvc-services
usvc data validate
usvc data run-tests
```

See [unitysvc-services documentation](https://github.com/unitysvc/unitysvc-services) for details.
