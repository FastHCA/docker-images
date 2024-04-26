# https://hub.docker.com/r/tarantool/tarantool

ARG IMAGE_BASE="tarantool/tarantool"
ARG IMAGE_TAG="3.1.0"

FROM ${IMAGE_BASE}:${IMAGE_TAG}

# compile lua-bigdecimal
ARG LUA_BIGDECIMAL_VERSION="0.1.1"
RUN apt-get update && \
    apt-get install -y build-essential curl lua5.1 lua5.1-dev && \
    cd /opt && \
    # 下載並解壓縮 lua-bigdecimal
    curl -fSL https://github.com/FastHCA/lua-bigdecimal/archive/refs/tags/v${LUA_BIGDECIMAL_VERSION}.tar.gz -o lua-bigdecimal-v${LUA_BIGDECIMAL_VERSION}.tar.gz && \
    tar xzf lua-bigdecimal-v${LUA_BIGDECIMAL_VERSION}.tar.gz && \
    cd /opt/lua-bigdecimal-${LUA_BIGDECIMAL_VERSION} && \
    # 編譯 lua-bigdecimal
    make all LUA_INCLUDE_DIR=/usr/include/lua5.1 LUA_LIBRARIES=/usr/lib/x86_64-linux-gnu && \
    # 確保目標位置存在並複製編譯後的模組到目標位置
    mkdir -p /usr/local/lib/tarantool/ && \
    cp bigdecimal.so /usr/local/lib/tarantool/bigdecimal.so
