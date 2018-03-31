# raspberry_tools

# mailip install

sudo apt-get install dnsutils curl postfix mailutils libsasl2-2 ca-certificates libsasl2-modules

sudo vim /etc/postfix/main.cf

relayhost = [smtp.gmail.com]:587
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_sasl_security_options = noanonymous
smtp_tls_CAfile = /etc/postfix/cacert.pem
smtp_use_tls = yes

sudo vim /etc/postfix/sasl_passwd

[smtp.gmail.com]:587    USERNAME@gmail.com:PASSWORD

sudo chmod 400 /etc/postfix/sasl_passwd
sudo postmap /etc/postfix/sasl_passwd

cat /etc/ssl/certs/thawte_Primary_Root_CA.pem | sudo tee -a /etc/postfix/cacert.pem
OR
cat ./raspberry_tools/Thawte_Premium_Server_CA.pem | sudo tee -a /etc/postfix/cacert.pem

sudo /etc/init.d/postfix reload

echo "Test mail from postfix" | mail -s "Test Postfix" you@example.com

@reboot /home/pi/bin/raspberry_tools/mailip
0 * * * * /home/pi/bin/raspberry_tools/mailip
