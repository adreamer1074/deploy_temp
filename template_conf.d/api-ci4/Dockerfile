FROM public.ecr.aws/amazonlinux/amazonlinux:2023

# 基本パッケージ + PHP 8.3 + Nginx
RUN dnf update -y && \
    dnf install -y \
        nginx \
        php \
        php-cli \
        php-fpm \
        php-mbstring \
        php-mysqlnd \
        php-xml \
        php-json \
        php-gd \
        php-intl \
        php-bcmath \
        unzip git && \
    dnf clean all

RUN php --version
# Composer インストール
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# Nginx / PHP 設定コピー
COPY conf.d/nginx-api-ci4.conf /etc/nginx/conf.d/nginx.conf
COPY conf.d/php-fpm.conf /etc/php-fpm.conf
COPY conf.d/php.ini /etc/php.d/php_my.ini

RUN mkdir -p /run/php-fpm

# アプリ配置 (CodeIgniter4 を /api-ci4 にコピー)
#これはローカルです。本番の場合、変更してください
WORKDIR /var/www/html/api-ci4
# COPY . /var/www/html/api-ci4

EXPOSE 80

CMD ["/sbin/init"]

# Nginx と php-fpm を起動（テスト環境はこれを使う）
# CMD php-fpm -D && nginx -g 'daemon off;'
