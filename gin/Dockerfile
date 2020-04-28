FROM ubuntu:16.04
RUN apt-get update
RUN apt-get install -y curl unzip zip software-properties-common lib32stdc++6 lib32z1
RUN add-apt-repository ppa:webupd8team/java

RUN wget -O - http://debian.opennms.org/OPENNMS-GPG-KEY | sudo apt-key add -
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get update && apt-get install -y maven oracle-java8-installer
