FROM openjdk:8-jdk
MAINTAINER Jorge Izquierdo Ciges <jorizci@ebi.com>

ENV AZKABAN_VERSION=3.30.1

RUN git clone https://github.com/azkaban/azkaban.git && cd azkaban \
    && git checkout tags/$AZKABAN_VERSION \
    && ./gradlew distZip \
    && unzip /azkaban/azkaban-web-server/build/distributions/azkaban-web-server-${AZKABAN_VERSION}.zip -d /opt \
    && ln -s /opt/azkaban-web-server-${AZKABAN_VERSION} /opt/azkaban-web-server \
    && sed -i "s/&//" /opt/azkaban-web-server/bin/azkaban-web-start.sh \
    && mkdir -p /opt/azkaban-web-server/conf /opt/azkaban-web-server/extlib  /opt/azkaban-web-server/logs\
    && cd .. \
    && rm -r azkaban \
    && apt-get clean \
    && rm -rf \
    /var/lib/apt/lists/* \
    /tmp/* \
    /var/tmp/* \
    /usr/share/man \
    /usr/share/doc \
    /usr/share/doc-base

ADD conf/ /opt/azkaban-web-server/conf/
ADD keystore /opt/azkaban-web-server/keystore

EXPOSE 12321
EXPOSE 8443

WORKDIR /opt/azkaban-web-server

ENTRYPOINT [ "./bin/azkaban-web-start.sh" ]
#ENTRYPOINT [ "/bin/bash" ]
