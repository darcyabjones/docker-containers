# Dockerfile
# 2016-07-31

FROM darcyabjones/base

LABEL software="samtools"
LABEL version="1.3.1"
LABEL description="Reading/writing/editing/indexing/viewing SAM/BAM/CRAM format."
LABEL website="http://www.htslib.org/"
LABEL usage="docker run --rm darcyabjones/samtools"
MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>


USER root

ENV URL https://github.com/samtools/samtools/releases/download/1.3.1/samtools-1.3.1.tar.bz2
ENV BUILD_DIR /home/user/bin/samtools-1.3.1

RUN apt-get update && apt-get install -yq --no-install-recommends \
    libncurses5 libncurses5-dev \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

RUN wget -qO- $URL \
    | tar -C $(dirname $BUILD_DIR) -xjf - \
    && cd $BUILD_DIR \
    && $BUILD_DIR/configure \
    && make -f $BUILD_DIR/Makefile \
    && make -f $BUILD_DIR/Makefile install \
    && rm -rf -- $BUILD_DIR

USER user

CMD ["samtools"]

# Change workdir to /data
WORKDIR /data
