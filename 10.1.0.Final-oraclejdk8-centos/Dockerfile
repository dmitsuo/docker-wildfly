FROM davimss/docker-jdk:8

USER root

ENV WILDFLY_VERSION 10.1.0.Final
ENV WILDFLY_HOME /opt/wf
ENV JBOSS_HOME $WILDFLY_HOME
ENV PATH $WILDFLY_HOME/bin:$PATH
ENV WILDFLY_DOWN_FILE wildfly-$WILDFLY_VERSION.tar.gz

RUN set -x ; \
    mkdir -p $WILDFLY_HOME ; \
    cd $WILDFLY_HOME ; \
    curl -O http://download.jboss.org/wildfly/$WILDFLY_VERSION/$WILDFLY_DOWN_FILE ; \
    tar -xvf $WILDFLY_DOWN_FILE --strip-components=1 ; \
    rm -rf bin/*.bat ; \
    rm -rf bin/*.ps1 ; \
    rm -rf $WILDFLY_DOWN_FILE ; \
    echo -e "\nJAVA_OPTS=\"\$JAVA_OPTS -Duser.language=pt -Duser.country=BR -Duser.timezone=America/Belem\"" >> $WILDFLY_HOME/bin/standalone.conf ; \
    chown root:root -R /opt

WORKDIR $WILDFLY_HOME

# EXPOSE 8080 9990
EXPOSE 8080

CMD bin/standalone.sh -b=0.0.0.0 -bmanagement=0.0.0.0