# Base it on Ubuntu 16.04 (latest)
FROM registry.mindef.nl/docker/ubuntu:16.04
MAINTAINER Stefan van Gastel <scwj.v.gastel@mindef.nl>

# Install packages (PHP 7 and Apache)
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -q && apt-get -qqy install \
    git-core \
	supervisor \
	apache2 \
	libapache2-mod-php && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Add image configuration and scripts
ADD start-apache2.sh /start-apache2.sh

# Add supervisor config for webserver
ADD supervisord-apache2.conf /etc/supervisor/conf.d/supervisord-apache2.conf

# Add apache config to enable .htaccess and do some stuff you want
ADD apache_default /etc/apache2/sites-available/000-default.conf

# Make sure scripts are excutable and configure apache
RUN chmod 755 /*.sh && \
    echo "ServerName localhost" >> /etc/apache2/apache2.conf && \
    a2enmod rewrite

# Link docroot to /app
RUN mkdir -p /app && \
    rm -fr /var/www/html && \
    ln -s /app /var/www/html

# Create placeholder file with php info
RUN echo '<?php phpinfo(); ?>' > /app/index.php

#Expose ports
EXPOSE 80
CMD ["supervisord", "-n"]
