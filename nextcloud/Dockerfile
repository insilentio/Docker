FROM nextcloud:apache
RUN mkdir /etc/ssl/nextcloud
COPY certs/nextcloud.crt /etc/ssl/nextcloud/nextcloud.crt
COPY certs/nextcloud.key /etc/ssl/nextcloud/nextcloud.key
COPY setssl.sh /usr/local/bin/
RUN /usr/local/bin/setssl.sh nc_admin@youremail.ch nextcloud.local
RUN apt update
RUN apt -y install vim
RUN apt -y install cron
