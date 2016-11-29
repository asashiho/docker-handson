# Step 1: ベースイメージ取得 --Base Docker image
FROM debian:jessie

# Step 2: 作成者情報 --Maintainer profile
MAINTAINER asashiho@mail.asa.yokohama


# Step 3: 環境変数の設定 --Set Environment Variables
ENV NGINX_VERSION 1.11.6-1~jessie


# Step 4: NGINXのインストール --Install NGINX
RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
        && echo "deb http://nginx.org/packages/mainline/debian/ jessie nginx" >> /etc/apt/sources.list \
        && apt-get update \
        && apt-get install --no-install-recommends --no-install-suggests -y \
                                                ca-certificates \
                                                nginx=${NGINX_VERSION} \
                                                nginx-module-xslt \
                                                nginx-module-geoip \
                                                nginx-module-image-filter \
                                                nginx-module-perl \
                                                nginx-module-njs \
                                                gettext-base \
        && rm -rf /var/lib/apt/lists/*

# Step 5: ログの転送 --Forward request logs to Docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log

# Step 6:httpポートの転送 --Expose port 80 from the container to the host
EXPOSE 80

# Step 7:HTMLのデプロイ --Add HTML file from the host to the container
ADD html/ /usr/share/nginx/html/

# Step 8:nginxの実行 --Execute NGNIX
CMD ["nginx", "-g", "daemon off;"]

