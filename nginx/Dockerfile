FROM centos:centos7
MAINTAINER choc<qinghecao@outlook.com>

ENV TZ "Asia/Shanghai"
ENV NGINX_VERSION='1.12.2'

RUN yum -y update && \
    yum install -y gcc automake autoconf libtool make gcc-c++ wget openssl-devel zip vim unzip libxml2-devel net-tools && \
    yum clean all

RUN groupadd www && useradd -g www www

RUN cd /tmp/ && \
    wget "http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz" && \
    tar -zxf "nginx-${NGINX_VERSION}.tar.gz" && \
    cd "nginx-${NGINX_VERSION}" && \
    ./configure \
    --prefix=/usr/local/nginx \
    --with-http_ssl_module --with-http_sub_module --with-http_dav_module --with-http_flv_module \
    --with-http_gzip_static_module --with-http_stub_status_module --with-debug && \
    make && \
    make install

EXPOSE 80 443

ENTRYPOINT ["/usr/local/nginx/sbin/nginx"]
