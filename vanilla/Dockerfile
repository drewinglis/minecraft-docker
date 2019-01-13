FROM alpine

ARG MC_VERSION=1.12.2

RUN mkdir -pv /tmp
ADD get_mc_hash.sh /tmp/

RUN mkdir -pv /opt/minecraft /etc/minecraft

RUN adduser -DHs /sbin/nologin minecraft

RUN echo "eula=true" > /etc/minecraft/eula.txt

RUN apk add --update ca-certificates openjdk8-jre-base tzdata wget bash \
    && MC_SERVER_URL=https://launcher.mojang.com/v1/objects/`/tmp/get_mc_hash.sh ${MC_VERSION}`/server.jar \
    && test $? \
    && wget -O /opt/minecraft/minecraft_server.jar "${MC_SERVER_URL}" \
    && apk del --purge wget bash && rm -rf /var/cache/apk/* \
    && chown -R minecraft:minecraft /etc/minecraft /opt/minecraft

VOLUME /etc/minecraft

EXPOSE 25565

USER minecraft

WORKDIR /etc/minecraft

ENV _JAVA_OPTIONS '-Xms256M -Xmx1024M'

CMD ["java", "-jar", "/opt/minecraft/minecraft_server.jar", "nogui"]
