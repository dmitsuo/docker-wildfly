#FROM njmittet/alpine-wildfly:10.1.0.Final
FROM davimss/docker-jdk8

USER caos

ENV WILDFLY_VERSION 10.1.0.Final
ENV WILDFLY_HOME /opt/wildfly-$WILDFLY_VERSION
ENV JBOSS_HOME $WILDFLY_HOME
ENV PATH $WILDFLY_HOME/bin:$PATH
ENV STANDALONE standalone-full
ENV WILDFLY_DOWN_FILE wildfly-$WILDFLY_VERSION.tar.gz

RUN mkdir -p "$WILDFLY_HOME"

WORKDIR $WILDFLY_HOME

RUN set -x \
    && curl -O http://download.jboss.org/wildfly/$WILDFLY_VERSION/$WILDFLY_DOWN_FILE \
    && tar -xvf $WILDFLY_DOWN_FILE --strip-components=1 \
    && rm bin/*.bat \
    && rm bin/*.ps1 \
    && rm $WILDFLY_DOWN_FILE

ADD standalone-full.xml standalone/configuration/standalone-full.xml
ENV JAVA_OPTS="$JAVA_OPTS -Djboss.server.default.config=standalone-full.xml"
# ADD ojdbc6-11.2.0.3.0.jar standalone/deployments/ojdbc6-11.2.0.3.0.jar

EXPOSE 8080 9990

RUN bin/add-user.sh admin 123 --silent

CMD bin/standalone.sh

