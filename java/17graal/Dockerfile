# FROM --platform=$TARGETOS/$TARGETARCH oraclelinux:9

FROM --platform=linux/amd64 clearlinux:latest

LABEL author="Rune580" maintainer=""

LABEL org.opencontainers.image.source="https://github.com/Rune580/yolks"

RUN swupd bundle-add git \
    && useradd -d /home/container -m container \
    && mkdir -p graalvm/graalvm-17 /usr/lib64/graalvm/graalvm-17/ \
    && curl -sLO https://download.oracle.com/graalvm/17/latest/graalvm-jdk-17_linux-x64_bin.tar.gz \
    && tar -xf graalvm-jdk-17_linux-x64_bin.tar.gz --directory /usr/lib64/graalvm/graalvm-17/ --strip-components 1 \
    && cp /usr/lib64/graalvm/graalvm-17/bin/* /usr/bin/ \
    && rm graalvm-jdk-17_linux-x64_bin.tar.gz

USER container
ENV USER=container HOME=/home/container JAVA_HOME=/usr/lib64/graalvm/graalvm-17/
WORKDIR /home/container

COPY ./../entrypoint.sh /entrypoint.sh
CMD [ "/bin/bash", "/entrypoint.sh" ]