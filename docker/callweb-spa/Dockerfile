FROM amazonlinux:2023

ENV TZ=Asia/Tokyo

RUN yum -y update && \
    yum -y install nginx unzip git && \
    yum clean all

# Node.js & Angular CLI
RUN curl -sL https://rpm.nodesource.com/setup_16.x | bash -
RUN yum -y install nodejs
RUN npm install -g @angular/cli@16.2.10

# マウントされるディレクトリ
WORKDIR /var/www/callweb-spa     
# Angular dev server用
EXPOSE 4200                      
# Nginx用
EXPOSE 80                        

# Nginx設定（自分のDockerfileと同じディレクトリから）
# COPY spa-nginx.conf /etc/nginx/conf.d/default.conf

# distをNginxの公開ディレクトリに配置
# RUN cp -r /app/dist/* /usr/share/nginx/html/


CMD ["nginx", "-g", "daemon off;"]