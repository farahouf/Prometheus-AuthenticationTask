# Prometheus-AuthenticationTask
authentication (self-signed Certificate) between prometheus Server and target.
these are the steps i followed for the authentication (self-signed Certificate) between prometheus Server and target.

1. I created certificates on the target server using openSSL.
  sudo openssl req -new -newkey rsa:2048 -days 365 -nodes -x509 -keyout node_exporter.key -out node_exporter.crt -subj "/C=US/ST=California/L=Oakland/O=MyOrg/CN=localhost" -addext "subjectAltName = DNS:localhost"
2. I created a configuration file config.yml containing the certificate file and key file paths.
3. Updated the /etc/systemd/system/node_exporter.service to see the new config.yml file
4. I copied the certificate file from the target to the prometheus server
5. updated the configuration file of the prometheus prometheus.yml with the path to the node_exporter.crt file
6. I've created hash (i used apache2-utils) on the prometheus and insert the hash in the config.yml file at the target server
7. I've updated the prometheus configuration file with the new password (not hashed) under (basic_auth)
