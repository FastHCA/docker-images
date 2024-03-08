FROM ubuntu:18.04

ENV VERSION 7.0.1-enhancement

RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y build-essential curl \
    && curl -fSL https://github.com/FastHCA/predixy/archive/refs/tags/${VERSION}.tar.gz -o ${VERSION}.tar.gz \
    && tar xzf ${VERSION}.tar.gz \
    && cd predixy-${VERSION} \
    && make \
    && mv src/predixy /usr/local/bin \
    && mkdir -p /etc/predixy/conf

ADD conf /etc/predixy/conf

CMD ["/usr/local/bin/predixy", "/etc/predixy/conf/predixy.conf"]
