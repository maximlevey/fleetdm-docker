ARG FLEET_VERSION
FROM fleetdm/fleet:${FLEET_VERSION:-latest}

ARG FLEET_MYSQL_USERNAME
ARG FLEET_MYSQL_PASSWORD

ENV FLEET_MYSQL_USERNAME=${FLEET_MYSQL_USERNAME}
ENV FLEET_MYSQL_PASSWORD=${FLEET_MYSQL_PASSWORD}

ENV FLEET_SERVER_ADDRESS 0.0.0.0:8080
ENV FLEET_MYSQL_ADDRESS mysql:3306
ENV FLEET_REDIS_ADDRESS redis:6379

ENV FLEET_LOGGING_JSON=true
ENV FLEET_LOGGING_DEBUG=true

ENV FLEET_SERVER_CERT=/tmp/server.cert
ENV FLEET_SERVER_KEY=/tmp/server.key

USER root

COPY secrets/certificate.pem ${FLEET_SERVER_CERT}
COPY secrets/certificate.key ${FLEET_SERVER_KEY}

RUN chmod 644 ${FLEET_SERVER_CERT} ${FLEET_SERVER_KEY}

EXPOSE 8080

USER fleet

CMD ["sh", "-c", "/usr/bin/fleet prepare db --no-prompt && /usr/bin/fleet serve"]