FROM ubuntu
USER root

RUN apt-get update && apt-get install -y git && \
    git clone https://github.com/hippo82/rtorrent-rutorrent-shared.git a && \
	git clone https://github.com/hippo82/rtorrent-plugins.git plugins && \
	git clone https://github.com/hippo82/ruTorrent-Themes.git themes && \
    cp ./a/extra.list /etc/apt/sources.list.d/extra.list && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y rtorrent tar gzip unzip rar zip unrar mediainfo curl php-fpm php-cli php-geoip nginx wget ffmpeg supervisor php-xml libarchive-zip-perl libjson-perl libxml-libxml-perl irssi sox && \
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
	unzip -o ./themes/themes.zip -d /var/www/rutorrent/plugins/theme/themes/ && \
	unzip -o ./plugins/plugins.zip -d /var/www/rutorrent/plugins/ && \
	rm -rf ./themes && \
	rm -rf ./plugins && \
    sed -i 's/\/var\/log/\/downloads\/\.log/g' /etc/nginx/nginx.conf


EXPOSE 80/tcp 443/tcp 49160/udp 49161/tcp 49161/udp
VOLUME /downloads

CMD ["supervisord"]

