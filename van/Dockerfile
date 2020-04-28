[07:48] Srikar  Kulkarni
    
FROM ubuntu:latest


RUN apt-get update && apt-get dist-upgrade -y && apt-get install -y wget
ENV TZ=America/New_York
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone


RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" -P /opt http://download.oracle.com/otn-pub/java/jdk/6u29-b11/jdk-6u29-linux-x64.bin
RUN chmod +x /opt/jdk-6u29-linux-x64.bin


WORKDIR /opt
RUN ./jdk-6u29-linux-x64.bin
ENV JAVA_HOME=/opt/jdk1.6.0_29
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









