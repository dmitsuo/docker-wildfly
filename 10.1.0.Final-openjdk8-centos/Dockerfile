#FROM njmittet/alpine-wildfly:10.1.0.Final
FROM davimss/docker-jdk8

USER caos

ENV WILDFLY_VERSION 10.1.0.Final
ENV WILDFLY_HOME /opt/wildfly-$WILDFLY_VERSION
ENV JBOSS_HOME $WILDFLY_HOME
ENV PATH $WILDFLY_HOME/bin:$PATH
ENV WILDFLY_DOWN_FILE wildfly-$WILDFLY_VERSION.tar.gz
ENV CONFIG_FILE standalone-full.xml

RUN mkdir -p "$WILDFLY_HOME"

WORKDIR $WILDFLY_HOME

RUN set -x \
    && curl -O http://download.jboss.org/wildfly/$WILDFLY_VERSION/$WILDFLY_DOWN_FILE \
    && tar -xvf $WILDFLY_DOWN_FILE --strip-components=1 \
    && rm bin/*.bat \
    && rm bin/*.ps1 \
    && rm $WILDFLY_DOWN_FILE \
    && ln -s $WILDFLY_HOME /opt/wf

COPY $CONFIG_FILE standalone/configuration/$CONFIG_FILE
COPY standalone.conf bin/standalone.conf

EXPOSE 8080 9990

CMD bin/standalone.sh --server-config=$CONFIG_FILE -b 0.0.0.0

