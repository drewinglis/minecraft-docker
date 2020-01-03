ARG VANILLA_CONTAINER

# TODO: Support MC versions other than 1.12.
FROM ${VANILLA_CONTAINER}:1.12

# Source this from https://github.com/gnembon/carpetmod112/releases
ARG CARPET_VERSION=v19_01_07

USER root

# Pull carpet patch files.
# TODO: Support MC versions other than 1.12.
RUN apk add --update wget zip \
    && wget -O /tmp/carpet.zip "https://github.com/gnembon/carpetmod112/releases/download/${CARPET_VERSION}/Carpetmod_${CARPET_VERSION}.zip"

# Prepare the code for patching.
RUN mkdir -pv /tmp/carpet && unzip -q /tmp/carpet.zip -d /tmp/carpet/

# Do the patching.
RUN zip -qu `find /tmp/carpet -name '*'`

# Clean up unneeded packages.
RUN apk del --purge wget zip \
    && rm -rf /var/cache/apk/*

USER minecraft
