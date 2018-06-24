FROM openjdk:8u131-jre-alpine
MAINTAINER Maksim Kostromin https://github.com/daggerok
RUN apk --no-cache add busybox-suid bash curl \
 && addgroup application-group \
 && adduser -h /home/application -s /bin/bash -D -u 1025 application application-group
USER application
WORKDIR /home/application
VOLUME ["/home/app"]
ENV JAVA_OPTS=${java_opts}
ENTRYPOINT java ${JAVA_OPTS} -jar ./app.jar
EXPOSE 8080
HEALTHCHECK --timeout=2s --retries=22 CMD curl -f http://127.0.0.1:8080/actuator/health || exit 1
COPY --chown=application ./target/*.jar ./app.jar
