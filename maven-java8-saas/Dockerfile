FROM ubuntu:18.04
RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:ts.sch.gr/ppa
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get update && apt-get install -y curl oracle-java8-installer
ENV TZ=America/New_York
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN echo "javax.xml.accessExternalSchema = all" > /usr/lib/jvm/java-8-oracle/jre/lib/jaxp.properties
RUN mkdir /app
ENV JAVA_HOME=/usr/lib/jvm/java-8-oracle
# Ruby Stuff
#RUN gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys D39DC0E3
RUN  gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
RUN /bin/bash -c "curl -sSL https://get.rvm.io | bash -s stable"
# RUN /bin/bash -l -c "curl -L get.rvm.io | bash -s stable"
RUN /bin/bash -l -c "rvm install 2.3"
RUN /bin/bash -l -c "echo 'gem: --no-ri --no-rdoc' > ~/.gemrc"
RUN /bin/bash -l -c "gem install bundler --no-ri --no-rdoc"


# Maven stuff
ADD http://apache.cs.utah.edu/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz /opt/


WORKDIR /opt
RUN tar xvf /opt/apache-maven-3.3.9-bin.tar.gz


ENV PATH=/opt/apache-maven-3.3.9/bin:$PATH


# Build script stuff
WORKDIR /
ADD build_app.sh build_app.sh
RUN chmod a+x build_app.sh
CMD ./build_app.sh
