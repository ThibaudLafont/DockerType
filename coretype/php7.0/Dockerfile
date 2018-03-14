FROM php:7.1.13-apache
RUN docker-php-source extract \
	&& apt-get update && apt-get install -y \
        mysql-client libmysqlclient-dev nano libjpeg62-turbo-dev libpng12-dev \
    && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install pdo pdo_mysql gd \
	&& a2enmod rewrite \
	&& a2enmod ssl \
	&& docker-php-source delete

COPY php/php.ini /usr/local/etc/php/
COPY apache2/apache2.conf /etc/apache2/apache2.conf

RUN mkdir -p  /etc/apache2/from-host \
	&& echo "" >> /etc/apache2/apache2.conf \
    && echo "# Include the configurations from the host machine" >> /etc/apache2/apache2.conf \
    && echo "IncludeOptional from-host/*.conf" >> /etc/apache2/apache2.conf
