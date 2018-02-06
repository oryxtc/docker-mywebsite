FROM php:7.1-fpm
#COPY ./php.ini /usr/local/etc/php/
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bf \
	&& curl -o /etc/apt/sources.list http://mirrors.163.com/.help/sources.list.jessie \
	&& cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libmcrypt-dev \
		libpng12-dev \
		vsftpd \
		telnet \
	&& pecl install redis-3.1.5 \
	&& pecl install xdebug-2.5.5 \
	&& pecl install swoole-2.0.10 \
	&& docker-php-ext-install -j$(nproc) bcmath pdo pdo_mysql fileinfo zip \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
	&& docker-php-ext-enable redis xdebug swoole