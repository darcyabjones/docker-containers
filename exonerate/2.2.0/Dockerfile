# Dockerfile
# 2016-07-31

FROM darcyabjones/base

LABEL software="Exonerate"
LABEL version="2.2.0"
LABEL description="A generic tool for sequence alignment."
LABEL website="https://www.ebi.ac.uk/about/vertebrate-genomics/software/exonerate"
LABEL usage="docker run --rm darcyabjones/exonerate"
MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>


USER root

ENV URL http://ftp.ebi.ac.uk/pub/software/vertebrategenomics/exonerate/exonerate-2.2.0.tar.gz
ENV BUILD_DIR /home/user/bin/exonerate-2.2.0

RUN apt-get update && apt-get install -yq --no-install-recommends \
    libglib2.0-dev \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

RUN wget -qO- $URL \
    | tar -C $(dirname $BUILD_DIR) -zxf -  \
    && cd $BUILD_DIR \
    && $BUILD_DIR/configure \
    && make -f $BUILD_DIR/Makefile \
    && make -f $BUILD_DIR/Makefile install \
    && rm -rf -- $BUILD_DIR

USER user

CMD ["exonerate"]

# Change workdir to /data
WORKDIR /data
