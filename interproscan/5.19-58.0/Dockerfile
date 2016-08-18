# Dockerfile
# 2016-08-05

FROM darcyabjones:base

LABEL software="InterProScan"
LABEL version="5.19-58.0"
LABEL description="InterProScan is a sequence analysis application (nucleotide and protein sequences) that combines different protein signature recognition methods into one resource."
LABEL website="https://www.ebi.ac.uk/interpro/"
LABEL usage="docker run --rm darcyabjones/interproscan"
MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>

USER root

ENV URL ftp://ftp.ebi.ac.uk/pub/software/unix/iprscan/5/5.19-58.0/interproscan-5.19-58.0-64-bit.tar.gz
ENV BUILD_DIR /home/user/bin/interproscan-5.19-58.0-64-bit

RUN echo "deb http://ftp.de.debian.org/debian jessie-backports main" > /etc/apt/sources.list
RUN apt-get update && apt-get install -yq --no-install-recommends \
    python \
    openjdk-8-jre \
    && rm -rf /var/lib/apt/lists/*

RUN wget -qO- $URL.md5 | awk '{print $1}' > $(dirname $BUILD_DIR)/md5sum && \
    mkfifo /tmp/teedoff.$$; \
    wget -qO- $URL \
    | tee /tmp/teedoff.$$ \
    | tar -C $(dirname $BUILD_DIR) -zxf - & sleep 1; \
    md5sum < /tmp/teedoff.$$ | awk '{print $1}' | cmp $(dirname $BUILD_DIR)/md5sum \
    && rm /tmp/teedoff.$$ $(dirname $BUILD_DIR)/md5sum

USER user

CMD ["hisat2", "-h"]

# Change workdir to /data
WORKDIR /data
