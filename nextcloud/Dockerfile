FROM nextcloud:12.0.4-apache
MAINTAINER Jens Dürr <dev-dockerhub@jensomato.de>

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list \
    && apt-get update && apt-get install -y \
        supervisor \
        cron \
        ffmpeg \
        libmagickwand-dev \
        libgmp3-dev \
        smbclient \
        libsmbclient-dev \
#       LibreOffice \
    && rm -rf /var/lib/apt/lists/* \
    && ln -s "/usr/include/$(dpkg-architecture --query DEB_BUILD_MULTIARCH)/gmp.h" /usr/include/gmp.h \
    && docker-php-ext-install bz2 gmp \
    && pecl install imagick smbclient \
    && docker-php-ext-enable imagick smbclient \
    && mkdir /var/log/supervisord /var/run/supervisord \
    && echo "*/15 * * * * su - www-data -s /bin/bash -c \"php -f /var/www/html/cron.php\""| crontab - \
    && (crontab -l ; echo "*/30 * * * * su - www-data -s /bin/bash -c \"/var/www/html/occ preview:pre-generate\"")| crontab -

COPY supervisord.conf /etc/supervisor/supervisord.conf

CMD ["/usr/bin/supervisord"]
