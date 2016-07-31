# Dockerfile
# 2016-07-31

FROM darcyabjones/base

LABEL software="STAR"
LABEL version="2.5.0a"
LABEL description="RNA-seq aligner."
LABEL website="https://github.com/alexdobin/STAR"
LABEL usage="docker run --rm darcyabjones/star"
MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>


USER root

ENV REPO https://github.com/alexdobin/STAR.git
ENV BUILD_DIR /home/user/bin/star

RUN apt-get update && apt-get install -yq --no-install-recommends \
    git \
    libyaml-dev \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

RUN perl -MCPAN -e 'my $c = "CPAN::HandleConfig"; $c->load(doit => 1, autoconfig => 1); $c->edit(prerequisites_policy => "follow"); $c->edit(build_requires_install_policy => "yes"); $c->commit'
RUN cpan -i Set::IntervalTree

## Clone recursive to include star-fusion.
RUN git clone --recursive "$REPO" $BUILD_DIR \
    && cd $BUILD_DIR \
    && git checkout STAR_2.5.0a \
    && make STAR \
    && cp $BUILD_DIR/bin/Linux_x86_64/STAR* /usr/local/bin \
    && rm -rf -- $BUILD_DIR

USER user

CMD ["STAR"]

# Change workdir to /data
WORKDIR /data
