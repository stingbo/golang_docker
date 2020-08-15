FROM golang

# 修改镜像源
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak \
    && sed -i "s@http://deb.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list \
    && sed -i "s@security.debian.org/debian-security@mirrors.aliyun.com/debian-security@g" /etc/apt/sources.list \
    && cat /etc/apt/sources.list \
    && DEBIAN_FRONTEND=noninteractive apt-get update --fix-missing

RUN buildDeps=" \
    " \
    runtimeDeps=" \
        vim \
        curl \
        git \
        supervisor \
    " \
    && DEBIAN_FRONTEND=noninteractive apt-get install --assume-yes apt-utils -y $buildDeps $runtimeDeps --no-install-recommends \
    && /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo 'Asia/Shanghai' >/etc/timezone \
    && rm -r /var/lib/apt/lists/*

WORKDIR $GOPATH/src
#COPY ./start.sh /root/startup.sh
#ENV APP_FILE /root/startup.sh
#CMD $APP_FILE

ENV GO111MODULE="on"
ENV GOPROXY="https://goproxy.cn"

EXPOSE 8088
