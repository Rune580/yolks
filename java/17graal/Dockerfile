# FROM --platform=$TARGETOS/$TARGETARCH oraclelinux:9

FROM --platform=linux/amd64 clearlinux:latest

LABEL author="Rune580" maintainer=""

LABEL org.opencontainers.image.source="https://github.com/Rune580/yolks"

ENV JAVA_PKG=https://web.archive.org/web/20230208173917/https://oca.opensource.oracle.com/gds/GRAALVM_EE_JAVA17_22_3_1/graalvm-ee-java17-linux-amd64-22.3.1.tar.gz \
    JAVA_HOME=/usr/java/jdk-17

RUN swupd bundle-add git \
    && useradd -d /home/container -m container \
    && curl --retry 10 --output /tmp/jdk.tgz "$JAVA_PKG"  \
    && mkdir -p "$JAVA_HOME" \
    && tar --extract --file /tmp/jdk.tgz --directory "$JAVA_HOME" --strip-components 1 \
    && rm /tmp/jdk.tgz

USER container
ENV USER=container HOME=/home/container PATH=${JAVA_HOME}/bin:${PATH}
WORKDIR /home/container

COPY ./../entrypoint.sh /entrypoint.sh
CMD [ "/bin/bash", "/entrypoint.sh" ]