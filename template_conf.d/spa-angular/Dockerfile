FROM public.ecr.aws/amazonlinux/amazonlinux:2023

RUN dnf update -y && \
    dnf install -y \
        nginx \
        php \
        php-cli \
        php-fpm \
        unzip git && \
    dnf clean all

# Nginx 設定
COPY conf.d/nginx-spa-angular.conf /etc/nginx/conf.d/nginx.conf
COPY conf.d/php-fpm.conf /etc/php-fpm.conf
# ディレクトリ作成
RUN mkdir -p /run/php-fpm

# ビルド済み Angular の成果物を配置
#これはローカルです。本番の場合、変更してください
# WORKDIR /var/www/html/spa-angular
# COPY app/dist/app /var/www/spa-angular/www/html

# ビルド済み Angular の成果物を配置
# dist/spa-angular の中身を Nginx が参照できる場所にコピー
COPY dist/spa-angular /var/www/html/angular

EXPOSE 80

CMD ["/sbin/init"]

# Nginx と php-fpm を起動（テスト環境はこれを使う）
# CMD php-fpm -D && nginx -g 'daemon off;'

