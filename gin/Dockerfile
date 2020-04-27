FROM ubuntu:16.04
RUN rm -rf /etc/apt/sources.list.d/webupd8team-java.list
RUN apt-get update -y
RUN apt-get install -y curl unzip zip software-properties-common lib32stdc++6 lib32z1
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get update && apt-get install -y maven oracle-java8-installer
