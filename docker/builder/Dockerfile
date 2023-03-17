FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y tzdata && \
    apt install -y g++ gcc make git wget pkg-config python3-dev python3-pip && \
    python3 -m pip install conan==1.58.0

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN wget https://go.dev/dl/go1.20.2.linux-arm64.tar.gz && \
    tar --strip-components=1 -xvf go1.20.2.linux-arm64.tar.gz  -C /usr/local && \
    echo "PATH=$PATH:/usr/local/go/bin" >> /etc/bash.bashrc

RUN wget https://cmake.org/files/v3.24/cmake-3.24.3-linux-aarch64.tar.gz && \
    tar --strip-components=1 -xvf cmake-3.24.3-linux-aarch64.tar.gz  -C /usr/local

RUN wget https://github.com/xianyi/OpenBLAS/releases/download/v0.3.21/OpenBLAS-0.3.21.tar.gz && \
    tar xvf OpenBLAS-0.3.21.tar.gz && \
    cd OpenBLAS-0.3.21 && cmake -B build && cd build && make -j && make install && \
    mkdir -p OpenBLAS-0.3.21/build && cd OpenBLAS-0.3.21/build && cmake ../ && make -j && make install && cd -

RUN wget https://github.com/confluentinc/librdkafka/archive/refs/tags/v2.0.2.tar.gz && \
    tar xvf v2.0.2.tar.gz && \
    mkdir -p librdkafka-2.0.2/build && cd librdkafka-2.0.2/build &&cmake ../ && make -j && make install && cd -

RUN git clone https://github.com/milvus-io/milvus.git && \
    cd milvus && git checkout 9950cacd102d1518833bfc55251f1e05343bdc17 && \
    sed -i 's/github.com\/confluentinc\/confluent-kafka-go\/kafka/github.com\/confluentinc\/confluent-kafka-go\/v2\/kafka/g' $(find -name *.go) && \
    sed -i 's/github.com\/confluentinc\/confluent-kafka-go v1.9.1/github.com\/confluentinc\/confluent-kafka-go\/v2 v2.0.2/g' go.mod && \
    sed -i '143a github.com\/confluentinc\/confluent-kafka-go\/v2 v2.0.2\/go.mod h1:qWGwym8EpAsIP5lZsTKhYTnYSGqkbxEfRB4A489Jo64=' go.sum && \
    sed -i '143a github.com\/confluentinc\/confluent-kafka-go\/v2 v2.0.2 h1:YmUjjRp1mSTqTxtHQYMQKBLa2hfgIZz9PSqoSRDkwf4=' go.sum

RUN make install

WORKDIR /milvus/
