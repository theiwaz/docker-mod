# Base it on Alpine-linux(latest)
# FROM registry.mindef.nl/docker/alpine-linux:latest
FROM alpine:3.9
MAINTAINER ryan@famvdwal.net

# Install packages (PHP 5 and Apache)
RUN apk update
RUN apk add apache2 php7-apache2 supervisor

# Clean up
#RUN apt-get clean
#RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Listen to localhost servername
RUN echo "ServerName localhost" >> /etc/apache2/httpd.conf

# Add image configuration and scripts
ADD start-apache2.sh /start-apache2.sh

# Make sure scripts are excutable
RUN chmod 755 /*.sh

# Add supervisor config for webserver
# RUN mkdir /etc/supervisor.d/ /run/apache2
RUN mkdir /etc/supervisor.d/ 
ADD supervisord.conf /etc
ADD supervisord-apache2.conf /etc/supervisor.d/supervisord-apache2.conf

# Add apache config to enable .htaccess and do some stuff you want
ADD apache_default /etc/apache2/conf.d/000-default.conf
RUN sed -i 's@#LoadModule rewrite@LoadModule rewrite@g' /etc/apache2/httpd.conf

# Link docroot to /app
RUN mkdir -p /app && mkdir -p /var/www && rm -fr /var/www/html && ln -s /app /var/www/html

# Create placeholder file with php info
RUN echo '<?php phpinfo(); ?>' > /app/index.php

#Expose ports
EXPOSE 80
CMD ["supervisord", "-n"]


