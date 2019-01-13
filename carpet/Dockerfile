ARG MC_VERSION=1.12.2
ARG VANILLA_CONTAINER_SRC

FROM ${VANILLA_CONTAINER_SRC}:${MC_VERSION}

# Source this from https://github.com/gnembon/carpetmod112/releases
ARG CARPET_VERSION=v19_01_07

RUN apk add --update wget \
    && wget -O /tmp/carpet.zip "https://github.com/gnembon/carpetmod112/releases/download/${CARPET_VERSION}/Carpetmod_${CARPET_VERSION}.zip" \
    && apk del --purge wget \
    && rm-rf /var/cache/apk/*

RUN unzip /tmp/carpet.zip
RUN unzip
