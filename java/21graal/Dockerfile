FROM --platform=linux/amd64 clearlinux:latest

LABEL author="Rune580" maintainer=""

LABEL org.opencontainers.image.source="https://github.com/Rune580/yolks"

ENV JAVA_PKG=https://download.oracle.com/graalvm/21/archive/graalvm-jdk-21.0.1_linux-x64_bin.tar.gz \
    JAVA_HOME=/usr/java/jdk-21

    RUN swupd bundle-add git \
    && useradd -d /home/container -m container \
    && JAVA_SHA256=$(curl "$JAVA_PKG".sha256) \
    && curl --output /tmp/jdk.tgz "$JAVA_PKG" \
    && echo "$JAVA_SHA256 */tmp/jdk.tgz" | sha256sum -c \
    && mkdir -p "$JAVA_HOME" \
    && tar --extract --file /tmp/jdk.tgz --directory "$JAVA_HOME" --strip-components 1 \
    && rm /tmp/jdk.tgz

USER container
ENV USER=container HOME=/home/container PATH=${JAVA_HOME}/bin:${PATH}
WORKDIR /home/container

COPY ./../entrypoint.sh /entrypoint.sh
CMD [ "/bin/bash", "/entrypoint.sh" ]