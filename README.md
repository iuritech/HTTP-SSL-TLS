# HTTP-SSL-TLS

1-

    sudo apt install apache2

2- alterar as tabelas hosts "www.simoes.com"

windows:

    c:\windows\systems32\drivers\etc\hosts

linux:

    /etc/hosts

3- instalar certificados raiz e intermedia no browser do windows

4- ativar modulo ssl do apache

    sudo a2enmod ssl
    sudo service apache2 restart

5- Crie um servidor virtual seguro, baseado em IP, cujo diretório raiz seja /var/www/simoes/ com index.html

Dica: ficheiro 

    /etc/apache2/sites-available/default-ssl.conf

subestituir - 

    <IfModule mod_ssl.c>
    <VirtualHost _default_:443>
    ServerName www.simoes.cb
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/simoes
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/www.simoes.com.csr.pem  
    SSLCertificateKeyFile /etc/ssl/private/www.simoes.com.key.pem
    </VirtualHost>
    </IfModule>

mover certificados

    cp /root/HTTP-SSL-TLS/certs/www.simoes.com.csr.pem /etc/ssl/certs/
    cp /root/HTTP-SSL-TLS/certs/www.simoes.com.key.pem /etc/ssl/private/

6- ativar virtual host

    sudo a2ensite default-ssl
    sudo service apache2 restart
