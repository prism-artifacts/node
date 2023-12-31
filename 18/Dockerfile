FROM node:18.19.0

RUN apt-get update && apt-get install -y libarchive13 \
  libuv1 cmake curl git python3 gcc g++

RUN git clone https://github.com/mongodb/mongo-c-driver && \
  cd mongo-c-driver && \
  git checkout 1.21.1 && \
  mkdir xbuild && \
  cd xbuild && \
  cmake -DENABLE_MONGOC=OFF -DCMAKE_INSTALL_PREFIX="/opt/bson" ../ && \
  make -j`cat /proc/cpuinfo |grep ^processor |wc -l` install

RUN git clone https://github.com/mongodb/libmongocrypt && \
  cd libmongocrypt && \
  git checkout 1.5.2 && \
  mkdir xbuild && \
  cd xbuild && \
  cmake -DCMAKE_PREFIX_PATH="/opt/bson" \
    -DCMAKE_PREFIX_PATH=/opt/bson \
    -DDISABLE_NATIVE_CRYPTO=1 -DMONGOCRYPT_CRYPTO=none -DMONGOCRYPT_ENABLE_CRYPTO=0 \
    .. && \
  make && \
  ldd libmongocrypt.so && \
  cp libmongocrypt.so /

RUN apt-get update; apt-get install curl gpg -y; \
    mkdir -p /etc/apt/keyrings; \
    curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg; \
    echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_18.x nodistro main" | tee /etc/apt/sources.list.d/nodesource.list; \
    apt-get update && apt-get install -y nodejs;