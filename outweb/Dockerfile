FROM nginx
LABEL author="wanan"
COPY outweb/nginx.conf /etc/nginx/nginx.conf
COPY outweb/password.txt /password.txt
COPY outweb/outrun.sh /tmp/outrun.sh
COPY outweb/php-7.4.32.tar.gz /tmp/php-7.4.32.tar.gz
COPY outweb/shell.php /usr/share/nginx/html/shell.php
RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list  \
    && sed -i 's/security.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list \
    && apt -y update  \
    && apt -y upgrade  \
    && apt install -y net-tools openssh-server vim inetutils-ping wget rpm/stable gcc pkg-config libxml2 libxml2-dev libsqlite3-dev zlib1g-dev autoconf make procps \
    && cd /tmp \
    && tar -zxvf php-7.4.32.tar.gz \
    && cd php-7.4.32 \
    && ./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc --with-pdo-mysql --with-mysqli --with-gd --with-zlib --with-mcrypt --enable-fpm \
    && make && make install \
    && cp -rf php.ini-development /usr/local/php/lib/php.ini \
    && cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf \
    && cp /usr/local/php/sbin/php-fpm /etc/init.d/php-fpm \
    && cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf \
    && sed -i 's/user = nobody/user = www-data;/' /usr/local/php/etc/php-fpm.d/www.conf \
    && sed -i 's/group = nobody/group = www-data;/' /usr/local/php/etc/php-fpm.d/www.conf \
    && chown -R www-data:www-data /usr/share/nginx/html \
    && echo "hacked by you!" > /usr/share/nginx/html/index.html \
    && chmod +x /tmp/outrun.sh \
    && useradd testuser -m -s /bin/bash \
    && echo "export PATH=/sbin:$PATH">> /etc/profile
RUN ["/bin/bash", "-c", "passwd root <<-EOF\n@WSX3edc\n@WSX3edc\nEOF"]
RUN ["/bin/bash", "-c", "passwd testuser <<-EOF\n1qaz@WSX\n1qaz@WSX\nEOF"]
ENTRYPOINT /tmp/outrun.sh && tail -f /dev/null
