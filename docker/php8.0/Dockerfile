FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

WORKDIR '/workspace'

RUN apt update \
    && apt upgrade -y \

    ## install dependencies
    && apt install -y lsb-release ca-certificates apt-transport-https software-properties-common git \
    && add-apt-repository ppa:ondrej/php \
    && apt update \
    && apt upgrade -y \

    ## install php
    && apt install -y php8.0-cli php8.0-dev php8.0-gd php8.0-curl php8.0-imap php8.0-mysql php8.0-mbstring php8.0-xml \
        php8.0-zip php8.0-bcmath php8.0-soap php8.0-intl php8.0-readline php8.0-msgpack php8.0-igbinary php8.0-ldap \
        php8.0-redis \

    # install composer
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \

    # install nodejs
    && curl -sL https://deb.nodesource.com/setup_14.x | bash - \
    && apt install -y nodejs \

    # cleaning
    && apt -y autoremove \
    && apt clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install composer
RUN composer global require laravel/installer

COPY start-container /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/start-container

ENTRYPOINT ["start-container"]
