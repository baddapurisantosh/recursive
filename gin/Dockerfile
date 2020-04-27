FROM ubuntu:latest

RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:webupd8team/java && \
    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections

//RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get update && apt-get install -y maven oracle-java8-installer
ENV TZ=America/New_York
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone


RUN echo "javax.xml.accessExternalSchema = all" > /usr/lib/jvm/java-8-oracle/jre/lib/jaxp.properties


RUN mkdir /app


ENV JAVA_HOME=/usr/lib/jvm/java-8-oracle
