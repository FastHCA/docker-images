# https://hub.docker.com/r/tarantool/tarantool

ARG IMAGE_BASE="tarantool/tarantool"
ARG IMAGE_TAG="2.11.0"

FROM ${IMAGE_BASE}:${IMAGE_TAG}

# compile lua-bigdecimal
ARG LUA_BIGDECIMAL_VERSION="0.1.1"
RUN apk add build-base \
    && apk add curl && apk add --upgrade curl \
    && apk add --upgrade lua5.1-dev \
    && cd /opt \
    && curl -fSL https://github.com/FastHCA/lua-bigdecimal/archive/refs/tags/v${LUA_BIGDECIMAL_VERSION}.tar.gz -o lua-bigdecimal-v${LUA_BIGDECIMAL_VERSION}.tar.gz \
    && tar xzf lua-bigdecimal-v${LUA_BIGDECIMAL_VERSION}.tar.gz \
    && cd /opt/lua-bigdecimal-${LUA_BIGDECIMAL_VERSION} \
    && make all \
        LUA_INCLUDE_DIR=/usr/include \
        LUA_LIBRARIES=/usr/lib \
    && cp bigdecimal.so /usr/local/lib/tarantool/bigdecimal.so
