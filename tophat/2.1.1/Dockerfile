# Dockerfile
# 2016-07-31

FROM darcyabjones/bowtie2:2.2.9

LABEL software="TopHat"
LABEL version="2.1.1"
LABEL description="A spliced read mapper for RNA-Seq."
LABEL website="http://www.htslib.org/"
LABEL usage="docker run --rm darcyabjones/tophat"
MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>


USER root

ENV URL https://ccb.jhu.edu/software/tophat/downloads/tophat-2.1.1.tar.gz
ENV BUILD_DIR /home/user/bin/tophat-2.1.1

RUN apt-get update && apt-get install -yq --no-install-recommends \
    libboost-dev \
    libboost-system-dev \
    libboost-thread-dev \
    python \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

RUN wget -qO- $URL \
    | tar -C $(dirname $BUILD_DIR) -zxf - \
    && cd $BUILD_DIR \
    && $BUILD_DIR/configure \
    && make -f $BUILD_DIR/Makefile \
    && make -f $BUILD_DIR/Makefile install \
    && rm -rf -- $BUILD_DIR

USER user

CMD ["tophat"]

# Change workdir to /data
WORKDIR /data
