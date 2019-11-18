FROM localhost:8082/centos-jdk8 AS gradle-base

ENV JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.232.b09-0.el7_7.x86_64
ENV PATH=$PATH:/opt/gradle/gradle-3.4.1/bin
ENV GRADLE_HOME=usr/local/opt/gradle/
RUN wget https://services.gradle.org/distributions/gradle-3.4.1-bin.zip
RUN mkdir /opt/gradle
RUN unzip -d /opt/gradle gradle-3.4.1-bin.zip
RUN export PATH=$PATH:/opt/gradle/gradle-3.4.1/bin
RUN echo $GRADLE_HOME
RUN echo $PATH
RUN gradle -v
