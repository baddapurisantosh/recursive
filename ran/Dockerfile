FROM ubuntu:latest
RUN apt-get update && apt-get install -y software-properties-common curl unzip
RUN add-apt-repository ppa:ts.sch.gr/ppa
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get update && apt-get install -y maven oracle-java8-installer
ENV TZ=America/New_York
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN echo "javax.xml.accessExternalSchema = all" > /usr/lib/jvm/java-8-oracle/jre/lib/jaxp.properties
RUN mkdir /app
ENV JAVA_HOME=/usr/lib/jvm/java-8-oracle

##### Beginning of New Relic Installation #####
RUN mkdir -p /opt/webserver
RUN curl -o /opt/newrelic.zip http://download.newrelic.com/newrelic/java-agent/newrelic-agent/current/newrelic-java.zip
RUN unzip /opt/newrelic.zip -d /opt/webserver 
RUN sed -ie "s/<%= license_key %>/${NEWRELIC_LICENSE}/g" /opt/webserver/newrelic/newrelic.yml
RUN sed -ie "s/My Application/${NEWRELIC_APPNAME}/g" /opt/webserver/newrelic/newrelic.yml
ENV NEW_RELIC_OPTS "-javaagent:/opt/webserver/newrelic/newrelic.jar"


ADD build_app.sh build_app.sh
RUN chmod a+x build_app.sh
CMD ./build_app.sh
