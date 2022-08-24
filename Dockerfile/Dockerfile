FROM php:7.4.24-fpm

RUN apt-get update -y && apt-get install -y openssl zip unzip git nano

# 安裝 Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN docker-php-ext-install pdo_mysql bcmath
RUN pecl install -o -f redis && docker-php-ext-enable redis

#COPY ./laravel.ini /usr/local/etc/php/conf.d
#COPY ./xlaravel.pool.conf /usr/local/etc/php-fpm.d/
#COPY ./php.ini /usr/local/etc/php/

# user 参数
ARG user=sokrates

# 安装依赖
RUN apt-get install -y sudo 

# 添加用户：赋予sudo权限，指定密码
RUN useradd --create-home --no-log-init --shell /bin/bash ${user} \
    && adduser ${user} sudo \
    && echo "${user}:80650390" | chpasswd

# 改变用户的UID和GID
# RUN usermod -u 1000 ${user} && usermod -G 1000 ${user}

# 指定容器起来的登录用户
USER ${user}

WORKDIR /var/www

EXPOSE 9000
