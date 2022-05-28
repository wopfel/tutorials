# systemd stuff

## Let's Encrypt certbot

Running certbot on a regular schedule.
I was running it *manually* for too long now. Time for a bit of automation.

File: `/etc/systemd/system/certbot-renewal.service`

```
[Unit]
Description=Certbot Renewal
[Service]
ExecStart=/usr/bin/certbot -q renew --post-hook "systemctl reload nginx"
```

File: `/etc/systemd/system/certbot-renewal.timer`

```
[Unit]
Description=Run certbot twice daily

[Timer]
OnCalendar=*-*-* 00,12:00:00
RandomizedDelaySec=12h
Persistent=true

[Install]
WantedBy=timers.target
```

Enable and check the timer by issuing following commands:

```
systemctl daemon-reload
systemctl enable --now certbot-renewal.timer
systemctl list-timers --all
journalctl -u certbot-renewal.service
systemctl status certbot-renewal.timer
```

The tiimer looks like this:

```
NEXT                         LEFT          LAST                         PASSED  UNIT                         ACTIVATES
Sun 2022-05-29 09:41:56 CEST 15h left      n/a                          n/a     certbot-renewal.timer        certbot-renewal.service
```
