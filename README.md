# `cloudflared` on FreeBSD

## Installation

1. [Set up Portsnap on FreeBSD](https://docs.freebsd.org/en/books/handbook/ports/#ports-using).

```zsh
portsnap fetch
portsnap extract
```

2. Install the [cloudflared port](https://www.freshports.org/net/cloudflared/):

```zsh
cd /usr/ports/net/cloudflared/ && make install clean
```

3. [Authenticate cloudflared](https://developers.cloudflare.com/cloudflare-one/applications/non-HTTP/ssh/ssh-connections#1-authenticate-cloudflared):

```zsh
cloudflared tunnel login
```

The `cert.pem` file should be moved to where `cloudflared` can find it e.g.
`/usr/local/etc/cloudflared`

4. Create `/usr/local/etc/cloudflared/config.yml`

```yaml
logfile: /var/log/cloudflared/cloudflared.log
url: ssh://localhost:22
hostname: ssh.example.com
```

5. Copy the [rc.d file](/rc.d/cloudflared) to `/usr/local/etc/rc.d`
6. Add `cloudflared_enable=YES` to `/etc/rc.conf`
7. Optionally, set up [short-lived certificates](https://developers.cloudflare.com/cloudflare-one/applications/non-HTTP/ssh/short-lived-certificates).
