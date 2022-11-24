FROM ubuntu:focal

ENV DEBIAN_FRONTEND noninteractive

ENV TERM=linux

ENV TZ=UTC

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
    && apt-get install -y --no-install-recommends gnupg \
    && mkdir -p ~/.gnupg \
    && chmod 600 ~/.gnupg \
    && echo "disable-ipv6" >> ~/.gnupg/dirmngr.conf \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E5267A6C \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C300EE8C \
    && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu focal main" > /etc/apt/sources.list.d/ppa_ondrej_php.list \
    && apt-get update \
    && apt-get -y --no-install-recommends install \
        sqlite3 \ 
        libsqlite3-dev \
        dialog \
        ca-certificates \
        apt-utils \
        curl \
        unzip \
        openssh-client \
        git 


# Install php
RUN apt-get -y --no-install-recommends install \ 
    php5.6 \
    php5.6-cli \
    php5.6-dev \
    php5.6-curl \
    php5.6-mbstring \
    php5.6-opcache \
    php5.6-readline \
    php5.6-xml \
    php5.6-zip \
    php5.6-bcmath \
    php5.6-mysql \
    php5.6-pgsql \
    php5.6-igbinary \
    php5.6-redis \
    php5.6-gd \
    php5.6-sqlite3 \
    php5.6-soap \
    php5.6-intl \
    php5.6-msgpack \
    php5.6-xdebug 

# FPM
RUN  apt-get -y --no-install-recommends install php5.6-fpm

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=1.10.26 

# Clear Cache
RUN composer clear-cache --quiet \
    && apt autoremove -y build-essential \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* \