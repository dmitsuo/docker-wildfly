#FROM njmittet/alpine-wildfly:10.1.0.Final
FROM openjdk:8-jdk

ENV WILDFLY_VERSION 10.1.0.Final
ENV WILDFLY_HOME /opt/wildfly-$WILDFLY_VERSION
ENV JBOSS_HOME $WILDFLY_HOME
ENV PATH $WILDFLY_HOME/bin:$PATH
ENV STANDALONE standalone-full
RUN mkdir -p "$WILDFLY_HOME"
WORKDIR $WILDFLY_HOME
COPY wildfly-$WILDFLY_VERSION.tar.gz wf.tar.gz
RUN set -x \
    && tar -xvf wf.tar.gz --strip-components=1 \
    && rm bin/*.bat \
    && rm bin/*.ps1 \
    && rm wf.tar.gz
ADD standalone-full.xml standalone/configuration/standalone-full.xml
ADD ojdbc6-11.2.0.3.0.jar standalone/deployments/ojdbc6-11.2.0.3.0.jar
EXPOSE 8080 9990
ENV JAVA_OPTS="$JAVA_OPTS -Djboss.server.default.config=standalone-full.xml -Duser.language=pt -Duser.country=BR -Duser.timezone=America/Belem -Djava.net.preferIPv4Stack=true"
RUN bin/add-user.sh admin 123 --silent
CMD bin/standalone.sh

