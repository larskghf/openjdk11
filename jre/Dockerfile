FROM debian:buster-slim as downloader

ARG DOWNLOADURL
ARG JAVAVERSION

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        apt-transport-https \
        ca-certificates \
        curl \
    && apt-get clean && apt-get autoremove && rm -Rf /var/lib/apt/lists/* && rm -Rf /var/cache/apt \
    && mkdir /tmp/jre-${JAVAVERSION} \
    && curl -L --silent ${DOWNLOADURL} | tar -xz --strip-components=1 -C "/tmp/jre-${JAVAVERSION}" \
    && rm -rf /tmp/jre-${JAVAVERSION}/demo/ /tmp/jre-${JAVAVERSION}/man/

#-----------------------------------------------------------------------------------------------------------------------
#-----------------------------------------------------------------------------------------------------------------------
FROM debian:buster-slim

ARG JAVAVERSION

ENV JAVA_HOME /opt/jre-${JAVAVERSION}/

COPY --from=downloader /tmp/jre-${JAVAVERSION} /opt/jre-${JAVAVERSION}

RUN update-alternatives --install /usr/bin/java java /opt/jre-${JAVAVERSION}/bin/java 100