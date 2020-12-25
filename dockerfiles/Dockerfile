FROM ubuntu:18.04
RUN apt update && apt install -y nginx net-tools vim
RUN rm -rf etc/nginx/sites-enabled/* /etc/nginx/conf.d/*
RUN mkdir /var/www/html/path2 && \
    mkdir /var/www/html/path1 && \
    echo "You have reached PATH1" >> /var/www/html/path1/index.html && \
    echo "You have reached PATH2" >> /var/www/html/path2/index.html && \
    chown -R www-data:www-data /var/www/html
COPY default.conf /etc/nginx/conf.d/default.conf
CMD service nginx start
CMD ["nginx","-g","daemon off;"]
