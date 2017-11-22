FROM ubuntu:16.04

MAINTAINER Patrick LUZOLO SIASIA

RUN apt-get update \
    && apt-get install -y locales \
    && locale-gen fr_FR.UTF-8

ENV LANG fr_FR.UTF-8
ENV LANGUAGE fr_FR:fr
ENV LC_ALL fr_FR.UTF-8

RUN apt-get update \
    && apt-get install -y curl zip unzip git software-properties-common supervisor sqlite3 --no-install-recommends \
    && add-apt-repository -y ppa:nginx/stable \
    && add-apt-repository -y ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y sudo nano htop git cron nginx vim gettext mysql-client php7.1-ldap \
       php7.1-fpm php7.1-cli php7.1-common php7.1-mcrypt php7.1-gd php7.1-mysql php7.1-json php7.1-zip \
       php7.1-pgsql php7.1-opcache php7.1-imap php-memcached php7.1-mbstring php7.1-xml php7.1-redis php7.1-intl php7.1-curl \
       php7.1-sqlite3 php7.1-xdebug \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && mkdir /run/php \
    && apt-get remove -y --purge software-properties-common \
    && apt-get -y autoremove \
    && apt-get clean \
    && apt-get autoclean \
    && echo -n > /var/lib/apt/extended_states \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && rm -rf /etc/cron.d/* \
    && rm -rf /etc/cron.hourly/* \
    && rm -rf /etc/cron.daily/* \
    && rm -rf /etc/cron.monthly/* \
    && rm -rf /usr/share/man/?? \
    && rm -rf /usr/share/man/??_* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf \
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

# Nginx config
ADD php-fpm.conf /etc/php/7.1/fpm/php-fpm.conf
ADD www.conf /etc/php/7.1/fpm/pool.d/www.conf

EXPOSE 9000
CMD ["php-fpm7.1"]
