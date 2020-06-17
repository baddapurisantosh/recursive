FROM ubuntu:18.04
RUN useradd -ms /bin/bash nativescript
COPY docker-entrypoint.sh /docker-entrypoint.sh

# Utilities
RUN apt-get update && \
    apt-get -y install apt-transport-https unzip curl usbutils --no-install-recommends && \
    rm -r /var/lib/apt/lists/*
# JAVA
# RUN apt-get update && \
#    apt-get -y install default-jdk --no-install-recommends && \
#    rm -r /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:ts.sch.gr/ppa
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get update && apt-get install -y maven oracle-java8-installer
ENV TZ=America/New_York
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN echo "javax.xml.accessExternalSchema = all" > /usr/lib/jvm/java-8-oracle/jre/lib/jaxp.properties
ENV JAVA_HOME=/usr/lib/jvm/java-8-oracle


# NodeJS
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get update && \
    apt-get -y install nodejs --no-install-recommends && \
    rm -r /var/lib/apt/lists/*

# NativeScript
RUN npm install -g nativescript && \
    tns error-reporting disable

# Android build requirements
RUN apt-get update && \
    apt-get -y install lib32stdc++6 lib32z1 --no-install-recommends && \
    rm -r /var/lib/apt/lists/*

# Android SDK
#ARG ANDROID_SDK_URL="https://dl.google.com/android/repository/tools_r25.2.5-linux.zip"
ARG ANDROID_SDK_URL="https://dl.google.com/android/repository/platform-tools-latest-linux.zip"
ARG ANDROID_SYSTEM_PACKAGE="android-25"
ARG ANDROID_BUILD_TOOLS_PACKAGE="build-tools-25.0.2"
ARG ANDROID_PACKAGES="platform-tools,$ANDROID_SYSTEM_PACKAGE,$ANDROID_BUILD_TOOLS_PACKAGE,extra-android-m2repository,extra-google-m2repository"
ADD $ANDROID_SDK_URL /tmp/android-sdk.zip
RUN mkdir /opt/android-sdk /app /dist && \
    chown nativescript:nativescript /tmp/android-sdk.zip /opt/android-sdk /app /dist
USER nativescript
ENV ANDROID_HOME /opt/android-sdk
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
RUN tns error-reporting disable && \
    unzip -q /tmp/android-sdk.zip -d /opt/android-sdk && \
    rm /tmp/android-sdk.zip && \
    echo "y" | /opt/android-sdk/tools/android --silent update sdk -a -u -t $ANDROID_PACKAGES
# Self-update of 'tools' package is currently not working?
#RUN echo "y" | /opt/android-sdk/tools/android --silent update sdk -a -u -t tools

VOLUME ["/app","/dist"]

WORKDIR /app

CMD ["/docker-entrypoint.sh"]
