FROM janej2013/milvus:builder-ubuntu20.04-openblas0.3.20-golang1.18 AS builder
FROM ubuntu:20.04

# change default shell for milvus users
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# keep same version with milvus builder images: milvus/build/docker/milvus/ubuntu18.04/Dockerfile
RUN apt-get update && \
    apt-get install -y --no-install-recommends libtbb-dev gfortran netcat iputils-ping ca-certificates libcurl4-openssl-dev && \
    apt-get remove --purge -y && \
    rm -rf /var/lib/apt/lists/*

COPY --from=builder /milvus/bin /milvus/bin/
COPY --from=builder /milvus/lib /milvus/lib/

# set environment variables to ensure that the program can run normally
ENV PATH=/milvus/bin:$PATH
ENV LD_LIBRARY_PATH=/milvus/lib:$LD_LIBRARY_PATH:/usr/lib

# set environment variables to ensure that the program can run normally
ENV PATH=/milvus/bin:$PATH
ENV LD_LIBRARY_PATH=/milvus/lib:$LD_LIBRARY_PATH:/usr/lib

WORKDIR /milvus/
