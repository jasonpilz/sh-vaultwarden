## Self-hosted Vaultwarden

> [Caddy with DNS Challenge](https://github.com/dani-garcia/vaultwarden/wiki/Using-Docker-Compose#caddy-with-dns-challenge)

### Bootstrap

1. Fill in `PRIVATE_IP_ADDRESS` in `.env`
2. Fill in `CLOUDFLARE_API_TOKEN` in `caddy/caddy.env`
3. Set up systemd (below)

### Cloudflare DNS Challenge

#### References

* [Cloudflare Config](https://github.com/AlphanAksoyoglu/vaultwarden-rpi?tab=readme-ov-file#cloudflare)
* [Cloudflare Setup](https://github.com/dani-garcia/vaultwarden/wiki/Running-a-private-vaultwarden-instance-with-Let%27s-Encrypt-certs#cloudflare-setup)
* [Cloudflare Dashboard](https://dash.cloudflare.com/38267d786336c199ab9994dc4fbebf23/jasonpilz.com/dns/records)
* [Cloudflare API Tokens](https://dash.cloudflare.com/profile/api-tokens)

#### DNS Record

Domain: _vaultwarden.jasonpilz.com_
Values: `A | vaultwarden | <PRIVATE_IP_ADDRESS> | DNS only - reserved IP | Auto`

#### API Token

Name: **Edit zone DNS Vaultwarden**
Settings: `jasonpilz.com - Zone:Read, DNS:Edit`

### Unifi Controller Configuration

> No port forwarding required with DNS challenge

### Systemd

**Reload and Enable Service**
```bash
sudo systemctl daemon-reload
sudo systemctl enable vaultwarden.service
sudo systemctl start vaultwarden.service
```

**Check Status
```bash
sudo systemctl status vaultwarden.service
```

**Check it Starts at Boot
```bash
sudo reboot
...
docker ps -a
```

**View Logs**
```bash
journalctl -u vaultwarden.service -f
```
