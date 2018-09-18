FROM php:7.2-fpm
COPY ./pecl /usr/local/pecl
RUN curl -o /etc/apt/sources.list.d/aliyun.list https://gist.githubusercontent.com/oryxtc/ba58ee12aebe92a4a8f1e9fb6baf69ea/raw/321c440618333ffb2fb2362ab939e9595c104cfb/aliyun.sources.list.jessie \
	&& cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN apt-get update && apt-get install -y \
		libssl-dev \
		zlib1g-dev \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libmcrypt-dev \
		libpng-dev \	
		librdkafka-dev \
	&& pecl install /usr/local/pecl/redis-4.0.0.tgz \
	&& pecl install /usr/local/pecl/xdebug-2.6.0.tgz \
	&& pecl install /usr/local/pecl/swoole-2.2.0.tgz \
	&& pecl install /usr/local/pecl/rdkafka-3.0.5.tgz \
	&& pecl install /usr/local/pecl/mongodb-1.5.0.tgz \
	&& pecl install /usr/local/pecl/yaf-3.0.7.tgz \
	&& rm /usr/local/pecl/redis-4.0.0.tgz  /usr/local/pecl/xdebug-2.6.0.tgz /usr/local/pecl/swoole-2.2.0.tgz \
	&& docker-php-ext-install -j$(nproc) bcmath pdo mysqli pdo_mysql fileinfo zip \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
	&& docker-php-ext-enable redis xdebug swoole rdkafka mongodb yaf