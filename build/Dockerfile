FROM registry.bizsaas.net/java:openjdk8-alpine
#MAINTAINER pader "huangmnlove@163.com"

# set environment
ENV MODE="cluster" \
    PREFER_HOST_MODE="ip"\
    BASE_DIR="/home/nacos" \
    CLASSPATH=".:/home/nacos/conf:$CLASSPATH" \
    CLUSTER_CONF="/home/nacos/conf/cluster.conf" \
    FUNCTION_MODE="all" \
    JAVA_HOME="/usr/lib/jvm/default-jvm" \
    NACOS_USER="nacos" \
    JAVA="/usr/lib/jvm/default-jvm/bin/java" \
    JVM_XMS="1g" \
    JVM_XMX="1g" \
    JVM_XMN="512m" \
    JVM_MS="128m" \
    JVM_MMS="320m" \
    NACOS_DEBUG="n" \
    TOMCAT_ACCESSLOG_ENABLED="false" \
    TIME_ZONE="Asia/Shanghai"

ARG NACOS_VERSION=2.1.2
#ARG HOT_FIX_FLAG=""

WORKDIR $BASE_DIR
#RUN sudo chown -R admin /home
#RUN set -x \
#    && yum update -y \
#    && yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel wget iputils nc  vim libcurl
#RUN wget  https://github.com/alibaba/nacos/releases/download/${NACOS_VERSION}${HOT_FIX_FLAG}/nacos-server-${NACOS_VERSION}.tar.gz -P /home
#RUN wget  https://file.devops.clickpaas.tech/software/nacos-server-${NACOS_VERSION}.tar.gz -P /home
RUN sudo apk add --no-cache libc6-compat tini busybox-extras bash curl openssh-client tzdata net-tools \
    && sudo ln -s /lib/libc.musl-x86_64.so.1 /lib/ld-linux-x86-64.so.2 \
    && sudo rm -rf /var/cache/apk/*

COPY nacos-server-${NACOS_VERSION}.tar.gz /home/
RUN sudo tar -xzvf /home/nacos-server-${NACOS_VERSION}.tar.gz -C /home \
    && sudo rm -rf /home/nacos-server-${NACOS_VERSION}.tar.gz /home/nacos/bin/* /home/nacos/conf/*.properties /home/nacos/conf/*.example /home/nacos/conf/nacos-mysql.sql
#RUN yum autoremove -y wget \
#    && ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime && echo $TIME_ZONE > /etc/timezone \
#    && yum clean all

ADD bin/docker-startup.sh bin/docker-startup.sh
ADD conf/application.properties conf/application.properties

# set startup log dir
RUN sudo chown -R admin /home \
    && mkdir -p logs \
	&& cd logs \
	&& touch start.out \
	&& ln -sf /dev/stdout start.out \
	&& ln -sf /dev/stderr start.out
RUN sudo chmod +x bin/docker-startup.sh


EXPOSE 8848
ENTRYPOINT ["bin/docker-startup.sh"]
