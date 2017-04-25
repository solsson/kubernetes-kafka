FROM openjdk:8-jre-alpine

ARG kafka_version=0.10.2.0
ENV kafka_bin_version=2.12-$kafka_version

RUN apk add --no-cache --update-cache --virtual build-dependencies curl ca-certificates \
  && mkdir -p /opt/kafka \
  && curl -SLs "https://www-eu.apache.org/dist/kafka/$kafka_version/kafka_$kafka_bin_version.tgz" | tar -xzf - --strip-components=1 -C /opt/kafka \
  && apk del build-dependencies \
  && rm -rf /var/cache/apk/*
FROM openjdk:8u102-jre

WORKDIR /opt/kafka
ENTRYPOINT ["bin/kafka-server-start.sh"]

ADD config/server.properties config/

CMD ["config/server.properties"]
