# FROM --platform=$TARGETOS/$TARGETARCH oraclelinux:9

FROM --platform=linux/amd64 clearlinux:latest

LABEL author="Rune580" maintainer=""

LABEL org.opencontainers.image.source="https://github.com/Rune580/yolks"

RUN swupd bundle-add git \
    && useradd -d /home/container -m container \
    && curl -sLO https://oca.opensource.oracle.com/gds/GRAALVM_EE_JAVA8_21_3_5/graalvm-ee-java8-linux-amd64-21.3.5.tar.gz \
    && tar -xf graalvm-ee-java8-linux-amd64-21.3.5.tar.gz \
    && mkdir -p graalvm/graalvm21-ee-8 /usr/lib64/graalvm/graalvm21-ee-8/ \
    && mv graalvm-ee-java8-21.3.5/* /usr/lib64/graalvm/graalvm21-ee-8/ \
    && rm -rf graalvm-ee-java8-21.3.5 \
    && rm graalvm-ee-java8-linux-amd64-21.3.5.tar.gz
# RUN swupd search lsof curl ca-certificates openssl git tar sqlite fontconfig freetype tzdata iproute stdc++

# RUN yum provides graalvm21

# RUN yum install -y lsof curl ca-certificates openssl git tar sqlite fontconfig freetype-devel tzdata iproute libstdc++ graalvm21-ee-8-jdk \
#     && useradd -d /home/container -m container

USER container
ENV USER=container HOME=/home/container JAVA_HOME=/usr/lib64/graalvm/graalvm21-ee-8
WORKDIR /home/container

COPY ./../entrypoint.sh /entrypoint.sh
CMD [ "/bin/bash", "/entrypoint.sh" ]
