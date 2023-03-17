FROM amazoncorretto:17

ENV WILDFLY_VERSION 26.1.3.Final
ENV WILDFLY_SHA1 24a53b7f8ea384001912c4be78339cce1e0e1955
ENV INSTALLAtion_DIR /opt/jboss
ENV JBOSS_HOME $INSTALLAtion_DIR/wildfly
ENV JBOSS_LAUNCH_IN_BACKGROUND true

USER root
ADD https://github.com/wildfly/wildfly/releases/download/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz /tmp/

RUN yum update -y \
      && yum install -y tar xz gzip shadow-utils \
      && mkdir -p $INSTALLAtion_DIR \
      && tar -xf /tmp/wildfly-$WILDFLY_VERSION.tar.gz \
      && mv ./wildfly-$WILDFLY_VERSION $INSTALLAtion_DIR \
      && mv $INSTALLAtion_DIR/wildfly-$WILDFLY_VERSION $INSTALLAtion_DIR/wildfly \
      && rm /tmp/wildfly-$WILDFLY_VERSION.tar.gz \
      && useradd -ms /bin/bash jboss \
      && chown -R jboss:0 $JBOSS_HOME \
      && chmod -R g+rw $JBOSS_HOME

user jboss
EXPOSE 8080
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
