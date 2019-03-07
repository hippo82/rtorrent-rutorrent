FROM ubuntu
USER root

RUN apt-get update && apt-get install -y git && \
    git clone https://github.com/hippo82/rtorrent-rutorrent-shared.git a && \
	git clone https://github.com/hippo82/rtorrent-plugins.git plugins && \
	git clone https://github.com/hippo82/ruTorrent-Themes.git themes && \
    cp ./a/extra.list /etc/apt/sources.list.d/extra.list && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y rtorrent tar gzip unzip unrar mediainfo curl php-fpm php-cli php-geoip nginx wget ffmpeg supervisor php-xml libarchive-zip-perl libjson-perl libxml-libxml-perl irssi sox && \
    rm -rf /var/lib/apt/lists/* && \
    cp ./a/rutorrent-*.nginx /root/ && \
    mkdir -p /var/www && \
    wget --no-check-certificate https://github.com/Novik/ruTorrent/archive/v3.8.tar.gz && \
    tar xzf v3.8.tar.gz && \
    mv ruTorrent-3.8 /var/www/rutorrent && \
    rm v3.8.tar.gz && \
    cp ./a/config.php /var/www/rutorrent/conf/ && \
    cp ./a/startup-rtorrent.sh ./a/startup-nginx.sh ./a/startup-php.sh ./a/startup-irssi.sh ./a/.rtorrent.rc /root/ && \
    cp ./a/supervisord.conf /etc/supervisor/conf.d/ && \
	cp -r ./plugins/ratiocolor /var/www/rutorrent/plugins/ && \
	cp -r ./themes/Agent34 /var/www/rutorrent/plugins/themes/themes/ && \
	cp -r ./themes/Agent46 /var/www/rutorrent/plugins/themes/themes/ && \
	cp -r ./themes/FlatUI_Dark /var/www/rutorrent/plugins/themes/themes/ && \
	cp -r ./themes/FlatUI_Light /var/www/rutorrent/plugins/themes/themes/ && \
	cp -r ./themes/FlatUI_Material /var/www/rutorrent/plugins/themes/themes/ && \
	cp -r ./themes/MaterialDesign /var/www/rutorrent/plugins/themes/themes/ && \
	cp -r ./themes/OblivionBlue /var/www/rutorrent/plugins/themes/themes/ && \
	cp -r ./themes/club-QuickBox /var/www/rutorrent/plugins/themes/themes/ && \
    sed -i 's/\/var\/log/\/downloads\/\.log/g' /etc/nginx/nginx.conf


EXPOSE 80/tcp 443/tcp 49160 49161
VOLUME /downloads

CMD ["supervisord"]

