FROM nextcloud:15.0.0-apache
MAINTAINER Jens Dürr <dev-dockerhub@jensomato.de>

RUN mkdir -p /usr/share/man/man1 \
    && apt-get update && apt-get install -y \
        supervisor \
        cron \
        ffmpeg \
	libbz2-dev \
        libgmp3-dev \
	libc-client-dev \
        smbclient \
        libsmbclient-dev \
#       LibreOffice \
    && rm -rf /var/lib/apt/lists/* \
    && ln -s "/usr/include/$(dpkg-architecture --query DEB_BUILD_MULTIARCH)/gmp.h" /usr/include/gmp.h \
    && docker-php-ext-install bz2 gmp \
    && pecl install smbclient \
    && docker-php-ext-enable smbclient \
    && mkdir /var/log/supervisord /var/run/supervisord \
    && echo 'memory_limit=512M' >> /usr/local/etc/php/conf.d/opcache-recommended.ini \
    && (crontab -l ; echo "*/30 * * * * su - www-data -s /bin/bash -c \"/var/www/html/occ preview:pre-generate\"")| crontab -

COPY supervisord.conf /etc/supervisor/supervisord.conf
ENV NEXTCLOUD_UPDATE=1
CMD ["/usr/bin/supervisord"]
