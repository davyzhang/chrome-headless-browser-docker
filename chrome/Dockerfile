FROM debian:stable-slim
# FROM ubuntu:xenial
# FROM google/debian:jessie

MAINTAINER Albert Yu <yukinying@gmail.com>

RUN apt-get update -qqy \
  && apt-get -qqy install \
       wget ca-certificates apt-transport-https \
       ttf-wqy-zenhei ttf-unfonts-core \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*
  
RUN mkdir -p /usr/share/man/man1 \
  && echo "deb http://http.debian.net/debian jessie-backports main" >> /etc/apt/sources.list.d/jessie-backports.list \
  && apt-get update -qqy \
  && apt-get -qqy --no-install-recommends install \
    -t jessie-backports openjdk-8-jre-headless \
    unzip \
    wget \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

RUN useradd headless --shell /bin/bash --create-home \
  && usermod -a -G sudo headless \
  && echo 'ALL ALL = (ALL) NOPASSWD: ALL' >> /etc/sudoers \
  && echo 'headless:nopassword' | chpasswd

RUN mkdir /data

ENTRYPOINT ["/usr/bin/google-chrome-unstable", \
            "--disable-gpu", \
            "--headless", \
            "--remote-debugging-address=0.0.0.0", \
            "--remote-debugging-port=9222", \
            "--user-data-dir=/data"]
