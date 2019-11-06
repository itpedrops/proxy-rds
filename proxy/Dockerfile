FROM nginx:latest
MAINTAINER PedrOps <pedro.silva@skyone.solutions>

RUN apt-get update

WORKDIR /home

ADD nginx.conf /etc/nginx/nginx.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
