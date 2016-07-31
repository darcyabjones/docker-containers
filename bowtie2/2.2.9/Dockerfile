#################################################################
# Dockerfile
#
# Version:          1
# Software:         Bowtie2
# Software Version: 2.0.4
# Description:      An ultrafast memory-efficient short read aligner.
# Website:          http://bowtie-bio.sourceforge.net/index.shtml
# Base Image:       darcyabjones:base
# Build Cmd:        docker build darcyjones/bowtie2 .
# Pull Cmd:         docker pull darcyabjones/bowtie2
# Run Cmd:          docker run darcyabjones/bowtie2
#################################################################

FROM darcyabjones/base

################## BEGIN INSTALLATION ###########################

USER root

ENV URL https://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.2.9/bowtie2-2.2.9-linux-x86_64.zip/download
ENV ARCHIVE_FILE /home/biodocker/bin/bowtie2-2.2.9-linux-x86_64.zip
ENV BUILD_DIR /home/biodocker/bin/bowtie2-2.2.9

RUN apt-get update && apt-get install -yq --no-install-recommends \
    unzip \
    && rm -rf /var/lib/apt/lists/*

RUN wget -qO $ARCHIVE_FILE $URL \
    && unzip -d $BUILD_DIR $ARCHIVE_FILE \
    && rm $ARCHIVE_FILE \
    && find $ARCHIVE_DIR -perm /a+x -type f -exec mv {} /usr/local/bin \; \
    && rm -rf -- $BUILD_DIR

USER biodocker

CMD ["bowtie"]

# Change workdir to /data
WORKDIR /data

##################### INSTALLATION END ##########################

# File Author / Maintainer
MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>
