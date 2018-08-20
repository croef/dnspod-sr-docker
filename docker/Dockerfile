FROM ubuntu:16.04

MAINTAINER croef, changrong185@gmail.com

RUN echo "deb http://mirrors.163.com/ubuntu/ xenial main restricted universe multiverse\ndeb http://mirrors.163.com/ubuntu/ xenial-security main restricted universe multiverse\ndeb http://mirrors.163.com/ubuntu/ xenial-updates main restricted universe multiverse\ndeb http://mirrors.163.com/ubuntu/ xenial-proposed main restricted universe multiverse\ndeb http://mirrors.163.com/ubuntu/ xenial-backports main restricted universe multiverse\ndeb-src http://mirrors.163.com/ubuntu/ xenial main restricted universe multiverse\ndeb-src http://mirrors.163.com/ubuntu/ xenial-security main restricted universe multiverse\ndeb-src http://mirrors.163.com/ubuntu/ xenial-updates main restricted universe multiverse\ndeb-src http://mirrors.163.com/ubuntu/ xenial-proposed main restricted universe multiverse\ndeb-src http://mirrors.163.com/ubuntu/ xenial-backports main restricted universe multiverse\n" > /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y vim make net-tools

RUN apt-get install -y git gcc
RUN git clone https://github.com/croef/dnspod-sr.git /home/src

WORKDIR /home/src/src
COPY config.h /home/src/src
RUN make
RUN mkdir -p /usr/local/services/dnspod-sr/bin \
	&& mv ./dnspod-sr /usr/local/services/dnspod-sr/bin

ENV PATH $PATH:/usr/local/services/dnspod-sr/bin

WORKDIR /root/dnspod
VOLUME ["/root/dnspod"]
COPY sr.conf /root/dnspod
COPY root.z /root/dnspod
COPY records.z /root/dnspod

WORKDIR /root/dnspod
CMD ["dnspod-sr"]
