FROM amritgc/nginx-php:latest

LABEL MAINTAINER="Amrit G.C. <music.demand01@gmail.com>"

ARG DOCKER_USER=homestead
ARG PUID=1000
ARG PGID=1000

RUN groupadd -g $PGID $DOCKER_USER && useradd -u $PUID -g $DOCKER_USER -m $DOCKER_USER && adduser $DOCKER_USER sudo


RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer
RUN chown homestead:homestead /usr/local/bin/composer


RUN curl -sL https://deb.nodesource.com/setup_8.x | bash && \
  apt-get install nodejs

# Enable php by default
#COPY default.conf /etc/nginx/conf.d/default.conf
COPY invoiceplane.conf /etc/nginx/sites-enabled/invoiceplane.conf
#ADD invoiceplane.conf /etc/nginx/conf.d/invoiceplane.conf

WORKDIR /var/www/

# Clone the project from git
RUN git clone https://github.com/invoiceplane/invoiceplane.git invoiceplane
WORKDIR /var/www/invoiceplane/
RUN git checkout v2.0.0
WORKDIR /var/www/

EXPOSE 80
CMD service php7.2-fpm start && nginx