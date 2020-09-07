# certbot-he-hook
Hook script helpers for obtaining [LetsEncrypt](https://letsencrypt.org/) certificates, using [Certbot](https://certbot.eff.org/) with [manual](https://certbot.eff.org/docs/using.html#manual) DNS-01 validation against [Hurricane Electric DNS](https://dns.he.net/).

## Example usage:

### With config:

1. Add either username/password or sessid credentials to the config file
```
HE_USER="<username>"
HE_PASS="<password>"
#HE_SESSID=""
```
2. To make this the default setting for Certbot, add the following to your Certbot config at `/etc/letsencrypt/cli.ini`
```
email = you@example.com
agree-tos = True
installer = None
server = https://acme-v02.api.letsencrypt.org/directory
authenticator = manual
preferred-challenges = dns-01
manual_auth_hook = /path/to/certbot-he-hook.sh
manual-cleanup-hook /path/to/certbot-he-hook.sh
manual-public-ip-logging-ok
```

3. Create a new certificate for a domain:
```
       certbot certonly \
         --domain <requested.domain.com>
```

4. Renew certificates for all domains:
```
       certbot renew
```

### Without configs:

1. Create a new certificate for a domain:
```
       HE_USER=<username> HE_PASS=<password> certbot certonly \
         --preferred-challenges dns \
         --email your@email.com \
         --manual \
         --manual-auth-hook /path/to/certbot-he-hook.sh  \
         --manual-cleanup-hook /path/to/certbot-he-hook.sh  \
         --manual-public-ip-logging-ok \
         --domain <requested.domain.com>
```

2. Renew certificates for all domains:
```        
       HE_USER=<username> HE_PASS=<password> certbot renew \
         --preferred-challenges dns \
         --manual-auth-hook /path/to/certbot-he-hook.sh  \
         --manual-cleanup-hook /path/to/certbot-he-hook.sh  \
         --manual-public-ip-logging-ok
```
