# Docker Milvus

## 1. Build base image

Before building milvus, we first need to build a base image that includes openblas (3.9+)

```bash
docker build -t soulteary/milvus-base:ubuntu20.04-openblas3.9 -f docker/base/Dockerfile .
```

[Advanced usage](./docs/01.build-openblas.md)

## 2. Build Milvus tools image

When we prepare the base image, we need to build a tool image that includes c++ and golang to build milvus in it.

```bash
docker build -t soulteary/milvus-builder:ubuntu20.04-openblas3.9 -f docker/builder/Dockerfile .
```

By default, we will get the latest Milvus code from GitHub, you can get the code from other data sources by adjusting the build parameters. [Advanced usage](./docs/02.build-builder.md)

## 3. Build a tiny Milvus Application image

TBD

## 4. Build a Milvus Application image with debugger

TBD