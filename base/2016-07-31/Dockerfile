# Dockerfile
# 2016-07-31

FROM debian:jessie

MAINTAINER Darcy Jones <darcy.ab.jones@gmail.com>


USER root

RUN apt-get update && apt-get install -yq --no-install-recommends \
    build-essential \
    ca-certificates \
    wget \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir /data /config

# Add user biodocker with password biodocker
RUN useradd --create-home --shell /bin/bash --user-group --uid 1000 user \
    && chown user:user /data \
    && chown user:user /config

# Change user
USER user

# Add $HOME/bin to path
ENV PATH=$PATH:/home/user/bin
ENV HOME=/home/user

# Create $HOME/bin folder
RUN mkdir /home/user/bin

# Share default volumes
VOLUME ["/data", "/config"]

CMD ["/bin/bash"]

# Change workdir to /data
WORKDIR /data
