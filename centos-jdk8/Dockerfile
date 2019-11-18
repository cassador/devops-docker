FROM localhost:8082/centos:7.7 AS java-base

RUN yum -y install java-1.8.0-openjdk-devel wget unzip
RUN ls -la /usr/lib/jvm
RUN export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.232.b09-0.el7_7.x86_64
RUN java -version
