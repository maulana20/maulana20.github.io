```bash
---------------------------------------------------------------------------
sudo apt install postfix mailutils
sudo systemctl status postfix
---------------------------------------------------------------------------
sudo nano /etc/postfix/main.cf
---------------------------------------------------------------------------
myhostname = fqdn.example.com
relayhost = smtp.mailtrap.io:2525
smtp_sasl_auth_enable = yes
smtp_sasl_mechanism_filter = plain
smtp_sasl_security_options = noanonymous
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
---------------------------------------------------------------------------
sudo cat /etc/postfix/sasl_passwd
sudo nano /etc/postfix/sasl_passwd
---------------------------------------------------------------------------
smtp.mailtrap.io:2525 username:password
---------------------------------------------------------------------------
postmap /etc/postfix/sasl_passwd
sudo /etc/init.d/postfix restart
---------------------------------------------------------------------------
echo "Test email body" | mail -s "Test email subject" no-reply@example.com
```
