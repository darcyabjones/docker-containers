# Dockerfile
# 2016-07-31

FROM darcyabjones/base

LABEL software="HISAT2"
LABEL version="2.0.4"
LABEL description="Graph-based alignment of next generation sequencing reads to a population of genomes."
LABEL website="https://ccb.jhu.edu/software/hisat2/index.shtml"
LABEL usage="docker run --rm darcyabjones/hisat2"
MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>


USER root

ENV URL ftp://ftp.ccb.jhu.edu/pub/infphilo/hisat2/downloads/hisat2-2.0.4-source.zip
ENV ARCHIVE_FILE /home/user/bin/hisat.zip
ENV BUILD_DIR /home/user/bin/hisat2-2.0.4

RUN apt-get update && apt-get install -yq --no-install-recommends \
    python \
    unzip \
    && rm -rf /var/lib/apt/lists/*

RUN wget -qO $ARCHIVE_FILE $URL \
    && unzip -d $(dirname $BUILD_DIR) $ARCHIVE_FILE \
    && rm $ARCHIVE_FILE \
    && cd  $BUILD_DIR \
    && make \
    && for f in $(find $BUILD_DIR -type f -executable | grep -v -P "\.h$|\.cpp$|scripts" -); do mv $f /usr/local/bin; done \
    && rm -rf -- $BUILD_DIR

USER user

CMD ["hisat2"]

# Change workdir to /data
WORKDIR /data
