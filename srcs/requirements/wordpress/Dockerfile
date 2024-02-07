FROM alpine:3.16

ARG PHP_VERSION=8
ARG DB_NAME
ARG DB_USER
ARG DB_PASS


RUN apk update && \
    apk upgrade && \
    apk add --no-cache \
    php${PHP_VERSION} \
    php${PHP_VERSION}-fpm \
    php${PHP_VERSION}-mysqli \
    php${PHP_VERSION}-json \
    php${PHP_VERSION}-curl \
    php${PHP_VERSION}-dom \
    php${PHP_VERSION}-exif \
    php${PHP_VERSION}-fileinfo \
    php${PHP_VERSION}-mbstring \
    php${PHP_VERSION}-openssl \
    php${PHP_VERSION}-xml \
    php${PHP_VERSION}-zip \
    php${PHP_VERSION}-redis \
    wget \
    unzip && \
    rm -rf /var/cache/apk/*

RUN sed -i "s|listen = 127.0.0.1:9000|listen = 9000|g" /etc/php${PHP_VERSION}/php-fpm.d/www.conf && \
    sed -i "s|;listen.owner = nobody|listen.owner = nobody|g" /etc/php${PHP_VERSION}/php-fpm.d/www.conf && \
    sed -i "s|;listen.group = nobody|listen.group = nobody|g" /etc/php${PHP_VERSION}/php-fpm.d/www.conf

WORKDIR /var/www


RUN wget -qO wordpress.zip https://wordpress.org/latest.zip && \
    unzip -q wordpress.zip && \
    cp -rf wordpress/* . && \
    rm -rf wordpress wordpress.zip


COPY ./requirements/wordpress/conf/wp-config-create.sh .
RUN chmod +x wp-config-create.sh && \
    ./wp-config-create.sh "${DB_NAME}" "${DB_USER}" "${DB_PASS}" && \
    rm wp-config-create.sh && \
    chmod -R 0777 wp-content/


CMD ["/usr/sbin/php-fpm${PHP_VERSION}", "-F"]
