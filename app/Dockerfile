#FROM richarvey/nginx-php-fpm
FROM webdevops/php-nginx:ubuntu-16.04

# git, curl already installed
# python3 missing (use py2 instead)
#
RUN set -x; \
  apt-get update \
  && apt-get install -y less vim python-pip python-dev libssl-dev libmysqlclient-dev jq mysql-client

ENV WEBROOT /var/www/public
ENV MEDIAWIKI_DIR /var/www/public/mediawiki

# REL1_29 REL1_28
ENV MEDIAWIKI_BRANCH master

WORKDIR /var/www/public/mediawiki

# Copy Nginx & MediaWiki config
#COPY ./conf/nginx/nginx-site.conf /etc/nginx/sites-enabled/default
COPY ./conf/nginx/vhost.conf /opt/docker/etc/nginx/vhost.conf

COPY ./conf/mediawiki/CustomSettings.php $WEBROOT/CustomSettings.php

COPY ./scripts /scripts

#get-data.sh /get-data.sh
#COPY cirrus2mysql.sh /cirrus2mysql.sh
COPY ./www $WEBROOT

# Restart nginx
# CMD supervisorctl restart nginx

# ADD elasticsearch.yml /usr/share/elasticsearch/config/
# USER root
# RUN chown elasticsearch:elasticsearch config/elasticsearch.yml
# USER elasticsearch

#COPY docker-entrypoint.sh /entrypoint.sh
#ENTRYPOINT ["/entrypoint.sh"]

# Cannot run install script (mysql, es are not avaialable at this stage)
#RUN /scripts/install_mediawiki.sh

#CMD ["supervisord"]
