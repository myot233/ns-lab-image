FROM gsycl2004/iis_experiment:base
COPY DVWA /var/www/localhost/htdocs
COPY supervisor.conf /etc/supervisor.d/default.ini

RUN ["apk","add","mariadb","mariadb-client","php83-apache2","firefox","nano","php83-session","php83-mysqli","php83-pdo","php83-pdo_mysql"]
RUN ["rm","/var/www/localhost/htdocs/index.html"]
RUN sed -i 's/Listen 80/Listen 8081/' /etc/apache2/httpd.conf
RUN sed w-i '/skip-networking/d' /etc/my.cnf.d/mariadb-server.cnf
# 使用 sed 修改 php.ini 配置
RUN sed -i 's/^display_errors = .*/display_errors = On/' /etc/php83/php.ini && \
    sed -i 's/^display_startup_errors = .*/display_startup_errors = On/' /etc/php83/php.ini && \
    sed -i 's/^allow_url_include = .*/allow_url_include = On/' /etc/php83/php.ini 


RUN mysql_install_db --user=mysql --datadir=/var/lib/mysql

RUN mysqld_safe & sleep 5 && mariadb -e "ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';CREATE DATABASE dvwa;" && kill $(pgrep mariadbd) # not work


