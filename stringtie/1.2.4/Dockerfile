# Dockerfile
# 2016-07-31

FROM darcyabjones/base

LABEL software="StringTie"
LABEL version="1.2.4"
LABEL description="Transcript assembly and quantification for RNA-Seq"
LABEL website="https://ccb.jhu.edu/software/stringtie/"
LABEL usage="docker run --rm darcyabjones/stringtie"
MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>


USER root

ENV URL http://ccb.jhu.edu/software/stringtie/dl/stringtie-1.2.4.tar.gz
ENV BUILD_DIR /home/user/bin/stringtie-1.2.4

RUN apt-get update && apt-get install -yq --no-install-recommends \
    python \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

RUN wget -qO- $URL \
    | tar -C $(dirname $BUILD_DIR) -zxf - \
    && cd  $BUILD_DIR \
    && make release \
    && mv $BUILD_DIR/stringtie /usr/local/bin \
    && rm -rf -- $BUILD_DIR

# Add python script for output to DESeq and EdgeR
RUN wget -qO- https://ccb.jhu.edu/software/stringtie/dl/prepDE.py > /usr/local/bin/prepDE.py \
    && chmod a+x /usr/local/bin/prepDE.py

USER user

CMD ["stringtie", "--help"]

# Change workdir to /data
WORKDIR /data
