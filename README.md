# Installing Penpot with docker-compose.

## Quick Installation

**Before starting the instance, direct the domain (subdomain) to the ip of the server where Penpot will be installed!**

## 1. Penpot Server Requirements
From and more
- 2 CPUs
- 2 RAM 
- 10 Gb 

Run for Ubuntu 22.04

``` bash
sudo apt-get purge needrestart
```

## 2.Install docker and docker-compose:

``` bash
curl -s https://raw.githubusercontent.com/6Ministers/penpot-docker-compose-for-prototypes-apps/master/setup.sh | sudo bash -s
```

## 3.Download Penpot instance:


``` bash
curl -s https://raw.githubusercontent.com/6Ministers/penpot-docker-compose-for-prototypes-apps/master/download.sh | sudo bash -s penpot
```

If `curl` is not found, install it:

``` bash
$ sudo apt-get install curl
# or
$ sudo yum install curl
```

Go to the catalog

``` bash
cd penpot
```
## 4. In the configuration file `docker-compose.penpot.env`, set the following parameters:

Install what you need, documentation:

https://help.penpot.app/technical-guide/configuration/

`PENPOT_FLAGS=`

``` bash
PENPOT_FLAGS=enable-registration enable-login disable-demo-users enable-email-verification enable-smtp enable-log-emails enable-login-with-password enable-prepl-server
```

- enable-cors: Enables the default cors cofiguration that allows all domains (this configuration is designed only for dev purposes right now).
- enable-backend-api-docs: Enables the /api/_doc endpoint that lists all rpc methods available on backend.
- enable-insecure-register: Enables the insecure process of profile registrion deactivating the - email verification process (only for local or internal setups).
- enable-user-feedback: Enables the feedback form at the dashboard.
- disable-secure-session-cookies: By default, penpot uses the secure flag on cookies, this flag disables it; it is usefull if you have plan to serve penpot under different domain than localhost without HTTPS.
- disable-login: allows disable password based login form.
- disable-registration: disables registration (still enabled for invitations only).
- enable-prepl-server: enables PREPL server, used by manage.py and other additional tools for communicate internally with penpot backend.


`PENPOT_PUBLIC_URI=`

``` bash
PENPOT_PUBLIC_URI=https://penpot.your-domain.com
```
I recommend installing SMTP so that you can confirm mail during registration, invite the team and send notifications.

``` bash
PENPOT_SMTP_DEFAULT_FROM=penpot@your-domain.com
PENPOT_SMTP_DEFAULT_REPLY_TO=penpot@your-domain.com
PENPOT_SMTP_HOST=smtp.your-domain.com
PENPOT_SMTP_PORT=465
PENPOT_SMTP_USERNAME=penpot@your-domain.com
PENPOT_SMTP_PASSWORD=
PENPOT_SMTP_TLS=false
PENPOT_SMTP_SSL=true
PENPOT_SMTP_DEFAULT_REPLY_TO=Penpot <no-reply@example.com>
PENPOT_SMTP_DEFAULT_FROM=Penpot <no-reply@example.com>
```


To change the domain in the `Caddyfile` to your own

``` bash
https://subdomain.your-domain:443 {
    header Strict-Transport-Security max-age=31536000;
    reverse_proxy 127.0.0.1:9001
    tls admin@example.org
	encode zstd gzip

...	
}
```

**Run Penpot:**

``` bash
docker-compose up -d
```

Then open `https://penpot.domain.com:` to access Penpot


## Penpot container management

**Run Penpot**:

``` bash
docker-compose up -d
```

**Restart**:

``` bash
docker-compose restart
```

**Restart**:

``` bash
sudo docker-compose down && sudo docker-compose up -d
```

**Stop**:

``` bash
docker-compose down
```

## Documentation
https://help.penpot.app/technical-guide/getting-started/
https://help.penpot.app/technical-guide/configuration/
