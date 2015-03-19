# Building.... / not yet completed.
FROM ubuntu:14.04

MAINTAINER Jioh L. Jung "ziozzang@gmail.com"

RUN echo "force-unsafe-io" > /etc/dpkg/dpkg.cfg.d/02apt-speedup
RUN echo "Acquire::http {No-Cache=True;};" > /etc/apt/apt.conf.d/no-cache
ENV DEBIAN_FRONTEND noninteractive
ENV HOME /root
ENV ZK_VERSION 3.4.6

RUN sed -i 's/archive.ubuntu.com/ftp.daum.net/g' /etc/apt/sources.list
RUN apt-get update && apt-get -y -o Dpkg::Options::="--force-confold" upgrade
RUN apt-get install -fy -qqy openjdk-7-jre-headless wget
RUN wget -q -O - http://apache.mirrors.pair.com/zookeeper/zookeeper-${ZK_VERSION}/zookeeper-${ZK_VERSION}.tar.gz | tar -xzf - -C /opt \
    && mv /opt/zookeeper-${ZK_VERSION} /opt/zookeeper \
    && cp /opt/zookeeper/conf/zoo_sample.cfg /opt/zookeeper/conf/zoo.cfg \
    && mkdir -p /tmp/zookeeper

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

EXPOSE 2181 2888 3888

WORKDIR /opt/zookeeper

VOLUME ["/opt/zookeeper/conf", "/tmp/zookeeper"]

ENTRYPOINT ["/opt/zookeeper/bin/zkServer.sh"]
CMD ["start-foreground"]
