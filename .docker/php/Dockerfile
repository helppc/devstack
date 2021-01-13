ARG composer=true
ARG development=false
FROM helppc/web-application:latest

ARG DEBIAN_FRONTEND=noninteractive
ARG composer
ARG development


COPY --chown=www-data ./application /var/www
COPY ./scheduler/ /etc/supervisor/conf.d/

WORKDIR /var/www

RUN rm -rf /var/www/.docker

RUN if [ "$composer" = "true" ] ; then if [ -f composer.json ] ; then  composer install --prefer-dist --ansi --no-progress --no-suggest; fi ; fi
RUN if [ "$development" = "true" ] ; then if [ -f composer.json ] ; then composer config extra.symfony.allow-contrib true; fi ; fi


RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
