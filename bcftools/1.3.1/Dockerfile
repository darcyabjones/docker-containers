# Dockerfile
# 2016-07-31

FROM darcyabjones/base

LABEL software="bcftools"
LABEL version="1.3.1"
LABEL description="Reading/writing BCF2/VCF/gVCF files and calling/filtering/summarising SNP and short indel sequence variants."
LABEL website="http://www.htslib.org/"
LABEL usage="docker run --rm darcyabjones/bcftools"
MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>


USER root

ENV URL https://github.com/samtools/bcftools/releases/download/1.3.1/bcftools-1.3.1.tar.bz2
ENV BUILD_DIR /home/user/bin/bcftools-1.3.1

RUN apt-get update && apt-get install -yq --no-install-recommends \
    libncurses5 libncurses5-dev \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

RUN wget -qO- $URL \
    | tar -C $(dirname $BUILD_DIR) -xjf - \
    && cd $BUILD_DIR \
    && make -f $BUILD_DIR/Makefile \
    && make -f $BUILD_DIR/Makefile install \
    && rm -rf -- $BUILD_DIR

USER user

CMD ["bcftools"]

# Change workdir to /data
WORKDIR /data
