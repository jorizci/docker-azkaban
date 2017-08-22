FROM openjdk:8-jdk
MAINTAINER Jorge Izquierdo Ciges <jorizci@ebi.com>

ENV AZKABAN_VERSION=3.30.1

RUN git clone https://github.com/azkaban/azkaban.git && cd azkaban \
    && git checkout tags/$AZKABAN_VERSION \
    && ./gradlew distZip \
    && pwd \
    && ls -la \
    && unzip /azkaban/azkaban-exec-server/build/distributions/azkaban-exec-server-${AZKABAN_VERSION}.zip -d /opt \
    && ln -s /opt/azkaban-exec-server-${AZKABAN_VERSION} /opt/azkaban-exec-server \
    && sed -i "s/&//" /opt/azkaban-exec-server/bin/azkaban-executor-start.sh \
    && mkdir -p /opt/azkaban-exec-server/conf /opt/azkaban-exec-server/extlib  /opt/azkaban-exec-server/logs\
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

EXPOSE 12321

ADD conf/ /opt/azkaban-exec-server/conf/
ADD plugins/ /opt/azkaban-exec-server/plugins/

WORKDIR /opt/azkaban-exec-server

ENTRYPOINT [ "./bin/azkaban-executor-start.sh" ]
