FROM debian:jessie-slim


RUN apt-get -y update && apt-get -yq install curl


RUN curl -ksSL https://github.com/openshift/origin/releases/download/v1.5.0/openshift-origin-client-tools-v1.5.0-031cbe4-linux-64bit.tar.gz \
    | tar -xzf - -C /opt && \
    ln -s /opt/openshift-origin-client-tools-v1.5.0-031cbe4-linux-64bit /opt/openshift-origin-client-tools


ENV PATH ${PATH}:/opt/openshift-origin-client-tools


ADD tag-to-image-stream.sh /tag-to-image-stream.sh


