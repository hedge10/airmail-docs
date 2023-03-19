# Getting started

## Installation

You can install _Airmail_ either locally or deploy it over a cloud service.

### Docker installation

Run the image directly

```shell
docker run ghcr.io/hedge10/airmail
```

Or use it with [Docker Compose](https://docs.docker.com/compose/) and paste this into your `docker-compose.yml`.

```yml
version: "3.9"

services:
  airmail:
    image: ghcr.io/hedge10/airmail
    ports:
      - "9900:9900"
```

### Local installation

Head over to the [releases page](https://github.com/hedge10/airmail/releases) on Github grab the version suitable for your operating system.

## Configuration

_Airmail_ is configured via environment variables. Please see the following reference for individual setup.

| Environment variable     | Default value | Description                                            |
| ------------------------ | :------------ | :----------------------------------------------------- |
| `AM_HOST`                | _none_        | IP address the web server listens on                   |
| `AM_PORT`                | `9900`        | Port the web server listens on                         |
| `AM_SMTP_HOST`           | `127.0.0.1`   | SMTP host                                              |
| `AM_SMTP_HOST`           | `25`          | SMTP port                                              |
| `AM_SMTP_USER`           | _none_        | SMTP username                                          |
| `AM_SMTP_PASS`           | _none_        | SMTP password                                          |
| `AM_SMTP_AUTH_MECHANISM` | `none`        | SMTP auth mechanism, possible options: `none`, `plain` |
| `AM_DEBUG`               | `false`       | Enable more logging output                             |
| `AM_ENV`                 | `dev`         | Set the stage airmail is running on                    |
| `AM_GRECAPTCHA_SECRET`   | _none_        | See [captcha section](messages.md#captcha-validation)  |
