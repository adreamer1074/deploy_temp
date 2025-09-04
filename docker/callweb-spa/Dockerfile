FROM amazonlinux:2023

ENV TZ=Asia/Tokyo

# 必要パッケージ + PHP 8.3 + Nginx
RUN yum -y update && \
    yum -y install nginx php8.3 php8.3-{cli,fpm,mysqlnd,zip,devel,gd,mbstring,xml,bcmath,intl} unzip git && \
    yum clean all

# Node.js 20.xインストール（ここが重要！）
RUN curl -sL https://rpm.nodesource.com/setup_20.x | bash -
RUN yum -y install nodejs

WORKDIR /var/www/callweb-spa

# 必要なら Angular CLI (グローバル)
RUN npm install -g @angular/cli@16.2.10

# Nginx設定
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./spa-nginx.conf /etc/nginx/conf.d/spa-nginx.conf

# .htpasswd（必要ならコピー）
COPY ./.htpasswd /etc/nginx/.htpasswd

RUN mkdir -p /run/php-fpm && chown nginx:nginx /run/php-fpm


EXPOSE 80

# PHP-FPMとNginxを両方起動
CMD ["/bin/bash", "-c", "php-fpm -D && nginx -g 'daemon off;'"]