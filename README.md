# clicmd

*List CloudLinux users by PHP version selector*
```shell
selectorctl --list-users --version=5.2
```

*Output IP info to imap logins from specific domain in `/var/log/maillog`
```shell
for i in $(zgrep domain.com /var/log/maillog* | grep imap-login | grep -v '127.0.0.1\|::1' | cut -d ',' -f 4 | cut -d '=' -f 2 | sort); do curl -s ipinfo.io/$i | grep 'ip\|city\|country\|org'; printf '%20s\n' | tr ' ' -; done
```

*Output imap login IP addresses (exclude local) connecting to specific domain*
```shell
zgrep domain.com /var/log/maillog* | grep imap-login | grep -v '127.0.0.1\|::1' | cut -d ',' -f 4 | cut -d '=' -f 2 | sort
```

*Output all unique IP logins using `dovecot_plain`*
```shell
grep "A=dovecot_plain" /var/log/exim_mainlog | sed -e 's#H=.* \[##' -e 's#\]:[0-9]*##' | awk '{print $6}' | sort -n | uniq
```

*Top 5 users sending emails on server*
```shell
grep "<=.*P=local" /var/log/exim_mainlog | awk '{print $6}' | sort | uniq -c | sort -nr | head -5 
```

*Output IP and number of failed attempts to send mail from server*
```shell
grep 'rejected RCPT' /var/log/exim_mainlog |awk '{print$4}'|awk -F\[ '{print $2} '|awk -F\] '{print $1} '|sort | uniq -c | sort -k 1 -nr | head -n 5
```

### Useful Links:
http://bradthemad.org/tech/notes/exim_cheatsheet.php
