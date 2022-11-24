FROM ghcr.io/zuzustack/php5.6:fpm

RUN apt-get update 

RUN apt install -y apache2
RUN apt-get install libapache2-mod-php5.6
RUN apt install libapache2-mod-fcgid -y

# RUN apt-get install supervisor -y

RUN apt clean

COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

COPY index.php /var/www/html
RUN rm /var/www/html/index.html

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

RUN a2dismod mpm_prefork && \ 
    a2dismod php5.6 

RUN a2enconf php5.6-fpm

RUN a2enmod proxy_fcgi proxy mpm_event rewrite

RUN echo "cgi.fix_pathinfo=1" >> /etc/php/5.6/fpm/php.ini

EXPOSE 80
# CMD ["apache2ctl", "-D", "FOREGROUND"]

CMD service php5.6-fpm start && apache2ctl -D FOREGROUND