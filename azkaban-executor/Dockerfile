FROM openjdk:8-jdk
MAINTAINER Jorge Izquierdo Ciges <jorizci@ebi.com>

ENV AZKABAN_VERSION=3.30.1

RUN git clone https://github.com/azkaban/azkaban.git && cd azkaban \
    && git checkout tags/$AZKABAN_VERSION \
    && ./gradlew distZip \
    && unzip /azkaban/azkaban-exec-server/build/distributions/azkaban-exec-server-${AZKABAN_VERSION}.zip -d /opt \
    && mv /opt/azkaban-exec-server-${AZKABAN_VERSION} /opt/azkaban-exec-server \
    && sed -i "s/&//" /opt/azkaban-exec-server/bin/azkaban-executor-start.sh \
    && sed -i "s/ &//" /opt/azkaban-exec-server/bin/start-exec.sh \
    && mkdir -p /opt/azkaban-exec-server/conf /opt/azkaban-exec-server/extlib  /opt/azkaban-exec-server/logs\
    && cd .. \
    && rm -rf azkaban \
    && rm -rf /root/.gradle \
    && rm -rf /root/.npm \
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

ENTRYPOINT [ "./bin/start-exec.sh" ]
