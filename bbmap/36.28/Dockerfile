# Dockerfile
# 2016-08-05

FROM darcyabjones/base

LABEL software="BBMap"
LABEL version="36.28"
LABEL description="BBMap short read aligner, and other bioinformatic tools."
LABEL website="https://sourceforge.net/projects/bbmap/"
LABEL usage="docker run --rm darcyabjones/bbmap"
MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>

USER root

ENV URL http://downloads.sourceforge.net/project/bbmap/BBMap_36.28.tar.gz
ENV BUILD_DIR /usr/local/bbmap

RUN apt-get update && apt-get install -yq --no-install-recommends \
    openjdk-7-jre openjdk-7-jdk \
    && rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64
RUN wget -qO - $URL \
    | tar -C $(dirname $BUILD_DIR) -zxf - \
    && cd $BUILD_DIR/jni \
    && make -f $BUILD_DIR/jni/makefile.linux

ENV PATH="$BUILD_DIR:${PATH}"

USER user

CMD ["bbmap.sh", "-h"]

# Change workdir to /data
WORKDIR /data
