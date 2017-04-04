FROM php:5-fpm
COPY sources.list /etc/apt/
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y apache2 libapache2-mod-fastcgi php-pear php5-fpm php5-mysqlnd php5-imagick imagemagick vim git curl wget net-tools python-software-properties software-properties-common make
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g" /etc/php5/fpm/php.ini
RUN sed -i "s 127.0.0.1:9000 /var/run/php5-fpm.sock g" /etc/php5/fpm/pool.d/www.conf
RUN a2enmod actions rewrite
RUN cp /etc/apache2/mods-enabled/fastcgi.conf /etc/apache2/mods-enabled/fastcgi.conf.backup
COPY fastcgi.conf /etc/apache2/mods-enabled/fastcgi.conf
WORKDIR /var/www/html
EXPOSE 80
#ENTRYPOINT service php5-fpm restart && service apache2 restart && chown www-data.www-data /var/run/php5-fpm.sock