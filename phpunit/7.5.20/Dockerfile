# PHPUnit Docker Container.
FROM alpine:3.8
LABEL mantainer="Rahul Prajapati <rahul.prajapati@live.in>"

LABEL name="phpunit-7.5.20"

ENV PEAR_PACKAGES foo

WORKDIR /tmp

RUN	echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    apk update && \
	apk upgrade && \
	apk add --update --no-cache \
        bash \
        ca-certificates \
        curl \
        git \
        subversion \
        php7 \
        php7-bcmath \
        php7-ctype \
        php7-curl \
        php7-dom \
        php7-exif \
        php7-fileinfo \
        php7-iconv \
        php7-json \
        php7-mbstring \
        php7-mcrypt \
        php7-mysqli \
        php7-opcache \
        php7-openssl \
        php7-pcntl \
        php7-pdo \
        php7-pdo_mysql \
        php7-pdo_pgsql \
        php7-pdo_sqlite \
        php7-phar \
        php7-session \
        php7-simplexml \
        php7-soap \
        php7-tokenizer \
        php7-xdebug \
        php7-xml \
        php7-xmlreader \
        php7-xmlwriter \
        php7-zip \
        php7-zlib \
        unzip \
        mariadb-client \
        php7-memcached \
        php7-phpdbg \
        sqlite-dev \
        wget \
    && php -r "copy('https://pear.php.net/go-pear.phar', 'go-pear.phar');" \
    && php go-pear.phar \
    && php -r "unlink('go-pear.phar');" \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/bin --filename=composer \
    && php -r "unlink('composer-setup.php');" \
    && composer require "phpunit/phpunit:7.5.20" --prefer-source --no-interaction \
    && composer require "phpunit/php-invoker" --prefer-source --no-interaction \
		&& composer require --dev yoast/phpunit-polyfills \
    && ln -s /tmp/vendor/bin/phpunit /usr/local/bin/phpunit \
    && sed -i 's/nn and/nn, Rahul Prajapati (Docker) and/g' /tmp/vendor/phpunit/phpunit/src/Runner/Version.php \
    # Enable X-Debug
    && sed -i 's/\;z/z/g' /etc/php7/conf.d/xdebug.ini \
    && php -m | grep -i xdebug

ONBUILD RUN \
    { \
        [ "${PEAR_PACKAGES}" != "foo" ]; \
    } || exit 0 && pear install ${PEAR_PACKAGES}

VOLUME ["/app"]

WORKDIR /app

CMD ["/bin/true"]
