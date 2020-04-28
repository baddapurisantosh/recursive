FROM ubuntu:latest
RUN apt-get update && apt-get dist-upgrade -y && apt-get install -y wget
ENV TZ=America/New_York
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
#RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" -P /opt "http://download.oracle.com/otn-pub/java/jdk/6u45-b06/jdk-6u45-linux-x64.bin"
#RUN wget --no-cookies --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2Ftechnetwork%2Fjava%2Fjavase%2Fdownloads%2Fjdk6-downloads-1637591.html;" -P /opt http://download.oracle.com/otn-pub/java/jdk/6u33-b03/jdk-6u33-linux-x64.bin

#RUN chmod +x /opt/jdk-6u33-linux-x64.bin
RUN apt-get install -y  curl
RUN curl  -L -C - -b "oraclelicense=accept-securebackup-cookie" -O -P /opt http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.tar.gz
WORKDIR /opt
#RUN tar -zxvf jdk-8u131-linux-x64.tar.gz
RUN tar xvzf /opt/jdk-8u131-linux-x64.tar.gz -C /opt
#RUN ./jdk-6u33-linux-x64.bin
ENV JAVA_HOME=/opt/jdk1.8.0_131
WORKDIR /


# Install Maven 2.2.1
ADD https://archive.apache.org/dist/maven/binaries/apache-maven-2.2.1-bin.tar.gz /opt
RUN tar xvzf /opt/apache-maven-2.2.1-bin.tar.gz -C /opt
ENV M2_HOME=/opt/apache-maven-2.2.1
ENV MAVEN_HOME=/opt/apache-maven-2.2.1
ENV PATH=$PATH:/opt/apache-maven-2.2.1/bin
RUN mkdir /app


#ENV JAVA_HOME=/usr/lib/jvm/java-6-oracle


ADD build_app.sh build_app.sh
RUN chmod a+x build_app.sh
CMD ./build_app.sh









