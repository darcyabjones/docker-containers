#################################################################
# Dockerfile
#
# Version:          1
# Software:         Trinity
# Software Version: 2.2.0
# Description:      Trinity RNA-Seq de novo transcriptome assembly.
# Website:          https://github.com/trinityrnaseq/trinityrnaseq
# Base Image:       darcyabjones:base
# Build Cmd:        docker build darcyjones/trinity .
# Pull Cmd:         docker pull darcyabjones/trinity
# Run Cmd:          docker run darcyabjones/trinity
#################################################################

FROM darcyabjones/base

################## BEGIN INSTALLATION ###########################

USER root

ENV TRINITY_URL https://github.com/trinityrnaseq/trinityrnaseq/archive/v2.2.0.tar.gz
ENV TRINITY_BUILD_DIR /home/user/bin/trinityrnaseq-2.2.0
ENV BOWTIE_URL http://downloads.sourceforge.net/project/bowtie-bio/bowtie/1.1.2/bowtie-1.1.2-src.zip
ENV BOWTIE_ARCHIVE_FILE /home/user/bin/bowtie-1.1.2-src.zip
ENV BOWTIE_BUILD_DIR /home/user/bin/bowtie-1.1.2

RUN apt-get update && apt-get install -yq --no-install-recommends \
    libtbb2 libtbb-dev \
    python \
    unzip \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

RUN wget -qO $BOWTIE_ARCHIVE_FILE $BOWTIE_URL \
    && unzip -d $(dirname $BOWTIE_BUILD_DIR) $BOWTIE_ARCHIVE_FILE \
    && cd $BOWTIE_BUILD_DIR \
    && make all \
    && make install \
    && rm $BOWTIE_ARCHIVE_FILE \
    && rm -rf -- $BOWTIE_ARCHIVE_FILE

RUN wget -qO- $TRINITY_URL \
    | tar -C $(dirname $TRINITY_BUILD_DIR) -zxf - \
    && cd $TRINITY_BUILD_DIR \
    && make all \
    && make plugins \
    && make test_all \
    && make test_clean \
    && rm -rf -- $TRINITY_BUILD_DIR

USER user

CMD ["Trinity", "-h"]

# Change workdir to /data
WORKDIR /data

##################### INSTALLATION END ##########################

# File Author / Maintainer
MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>
