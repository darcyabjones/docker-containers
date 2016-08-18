# Dockerfile
# 2016-08-05

FROM darcyabjones/base

LABEL software="Trimmomatic"
LABEL version="0.36"
LABEL description="A flexible read trimming tool for Illumina NGS data."
LABEL website="ab.org/cms/?page=trimmomatic"
LABEL usage="docker run --rm darcyabjones/trimmomatic"
MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>

USER root

ENV URL http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.36.zip
ENV ARCHIVE_FILE /home/user/bin/Trimmomatic-0.36.zip
ENV BUILD_DIR /usr/local/Trimmomatic-0.36

RUN echo "deb http://ftp.de.debian.org/debian jessie-backports main" >> /etc/apt/sources.list
RUN apt-get update && apt-get install -yq --no-install-recommends \
    openjdk-8-jre \
    unzip \
    && rm -rf /var/lib/apt/lists/*

RUN wget -qO $ARCHIVE_FILE $URL \
    && unzip -d $(dirname $BUILD_DIR) $ARCHIVE_FILE \
    && rm $ARCHIVE_FILE

COPY run.sh /usr/local/bin/trimmomatic
USER user

CMD ["trimmomatic", "-h"]

# Change workdir to /data
WORKDIR /data
