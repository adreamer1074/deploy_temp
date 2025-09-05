FROM amazonlinux:2023

ENV TZ=Asia/Tokyo

# 必要パッケージ + PHP 8.3 + Nginx
RUN yum -y update && \
    yum -y install nginx php8.3 php8.3-{cli,fpm,mysqlnd,zip,devel,gd,mbstring,xml,bcmath,intl} unzip git && \
    yum clean all

# Composerインストール
RUN cd /tmp && curl -sS https://getcomposer.org/installer | php \
&& mv ./composer.phar /usr/bin/composer
    
# PHP-FPM設定（カスタムファイルを必要に応じてコピー）
COPY ./php-fpm.conf /etc/php-fpm.conf
COPY ./www.conf /etc/php-fpm.d/www.conf

# Nginx設定
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./api-ci4-nginx.conf /etc/nginx/conf.d/api-ci4-nginx.conf
COPY ./php.ini /etc/php.ini

# ログ/セッションディレクトリ
RUN mkdir -p /var/log/php-fpm /var/log/nginx /var/lib/php/session
RUN mkdir -p /run/php-fpm && chown nginx:nginx /run/php-fpm


WORKDIR /var/www/callweb-api

EXPOSE 80

CMD ["bash", "-c", "php-fpm -D && nginx -g 'daemon off;'"]

# コマンドを使用出来るようにする
# 本番はsupervisordを使っている。これを使用。設定はsupervisord.confに。
# CMD ["/sbin/init"] 