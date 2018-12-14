FROM debian:jessie
MAINTAINER VenkyKuberan

ENV FILEBEAT_VERSION=5.6.1 \
    FILEBEAT_SHA1=91bdbaacee0034f9df9112fda2a25998e102d252

RUN set -x && \
  apt-get update && \
  apt-get install -y wget && \
  wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${FILEBEAT_VERSION}-linux-x86_64.tar.gz -O /opt/filebeat.tar.gz && \
  cd /opt && \
  echo "${FILEBEAT_SHA1}  filebeat.tar.gz" | sha1sum -c - && \
  tar xzvf filebeat.tar.gz && \
  cd filebeat-* && \
  cp filebeat /bin && \
  cd /opt && \
  rm -rf filebeat* && \
  apt-get remove wget -y && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY filebeat.yml /
CMD [ "filebeat", "-e", "-c=/filebeat.yml" ]