FROM ubuntu:16.04
RUN apt-get update
RUN apt-get install -y curl unzip zip software-properties-common lib32stdc++6 lib32z1
RUN echo "deb https://debian.opennms.org/ stable main" | tee /etc/apt/sources.list.d/webupd8team-java.list
RUN add-apt-repository ppa:webupd8team/java
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get update && apt-get install -y maven oracle-java8-installer
