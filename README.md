nginx-404.conf
=============

1) Add nginx-404.conf to /etc/fail2ban/filter.d

2) Add following to /etc/fail2ban/jail.conf

ignoreip = 127.0.0.1/8 ....
bantime  = 86400
findtime  = 900
maxretry = 5
usedns = no
destemail = root@domain
sender = fail2ban@domain
mta = sendmail
banaction = iptables-multiport
banaction_allports = iptables-allports

[nginx-404]
enabled = true
port = http,https
filter = nginx-404
logpath = <NGINX_ACCESS_PATH>
bantime = 600
findtime = 600
maxretry = 5

[wordpress]
enabled  = true
port     = http,https
filter   = wordpress-auth
logpath = %(nginx_error_log)s
maxretry = 3
bantime  = 3600

3) Adjust bantime/findtime/maxretry accordingly
