#
# Dockerizing MongoDB: Dockerfile for building MongoDB images
# Based on ubuntu:latest, installs MongoDB using the instructions from 
# http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/
#

FROM ubuntu:16.04

MAINTAINER Al Thompson <almacro@acm.org>

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.0 multiverse" > \
  /etc/apt/sources.list.d/mongodb-org-3.0.list
RUN apt-get update || echo ok

# install prereqs
RUN apt-get install -y \
  libboost-filesystem1.58.0 \
  libboost-program-options1.58.0 \
  libboost-system1.58.0 \
  libboost-thread1.58.0 \
  libgoogle-perftools4 \
  libpcap0.8 \
  libpcrecpp0v5 \
  libsnappy1v5 \
  libssl1.0.0 \
  libtcmalloc-minimal4 \
  libunwind8 \
  libv8-3.14.5 \
  libyaml-cpp0.5v5

COPY mongodb-linux-x86_64-ubuntu1604-3.2.8.tgz /
RUN  tar -C /tmp -xzf /mongodb-linux-x86_64-ubuntu1604-3.2.8.tgz && \
  cp -R -n /tmp/mongodb-linux-x86_64-ubuntu1604-3.2.8 /opt && \
  ln -s /opt/mongodb-linux-x86_64-ubuntu1604-3.2.8 /opt/mongodb && \
  rm /mongodb-linux-x86_64-ubuntu1604-3.2.8.tgz

RUN useradd mongo
RUN chown -R mongo /opt/mongodb-linux-x86_64-ubuntu1604-3.2.8
RUN mkdir -p /data/db
RUN chown -R mongo /data/db
VOLUME ["/data"]

EXPOSE 27017
USER mongo
ENTRYPOINT ["/opt/mongodb-linux-x86_64-ubuntu1604-3.2.8/bin/mongod", "--dbpath", "/data/db"]
