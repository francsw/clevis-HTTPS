# clevis-HTTPS
Get Clevis/Tang to work with HTTPS

# Assumptions
- This was tested on Ubuntu Focal (20.04)
- The SSL certificates are already installed on the Clevis client. Self signed also works.
- Use the same FQDN that there certificate was created for.
- Clevis uses curl to get the key from the tang server, so if it works with curl you're half way there, e.g. `curl -v https://tang01.lab.local:7500`
- You've setup some reverse proxy to use the SSL certificate on the Tang server.
- When you enroll the Tang key use https in your URL, e.g. 
`/usr/bin/clevis luks bind -f -d "/dev/sda3" tang '{"url":"https://tang01.lab.local:7500"}'`

# Setup initram to use the SSL certs
- Put the sslcerts script in `/usr/share/initramfs-tools/hooks/sslcerts`
- Recreate the initram
`/usr/sbin/update-initramfs -u -k 'all'`
