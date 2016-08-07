#
# This Dockerfile builds alpine-jdk8
#
FROM alpine

MAINTAINER Alfred Thompson <almacro@acm.org>

# install glibc-compat
COPY sgerrand.rsa.pub /etc/apk/keys
COPY glibc-2.23-r3.apk /tmp
RUN  cd /tmp && \
     apk add glibc-2.23-r3.apk && \
     rm /tmp/glibc-2.23-r3.apk

# install server-jre-8
COPY server-jre-8u101-linux-x64.tar.gz /tmp
RUN  mkdir /usr/java && \
     tar -C /usr/java -xf /tmp/server-jre-8u101-linux-x64.tar.gz && \
     ln -s /usr/java/jdk1.8.0_101 /usr/java/default && \
     rm /tmp/server-jre-8u101-linux-x64.tar.gz

# set up JAVA_HOME in system profile
COPY java /etc/profile.d

# enable strong encryption
COPY jce_policy-8.zip /tmp
RUN  cd /usr/java/jdk1.8.0_101/jre/lib/security && \
     unzip /tmp/jce_policy-8.zip && \
     mv US_export_policy.jar US_export_policy.jar,1 && \
     cp UnlimitedJCEPolicyJDK8/US_export_policy.jar . && \
     mv local_policy.jar local_policy.jar,1 && \
     cp UnlimitedJCEPolicyJDK8/local_policy.jar . && \
     rm -fr UnlimitedJCEPolicyJDK8

CMD /bin/sh