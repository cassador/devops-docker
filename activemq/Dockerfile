FROM openjdk:8-jre-alpine
#FROM rmohr/activemq
COPY apache-activemq-5.15.6-bin.tar.gz /apache-activemq-5.15.6-bin.tar.gz
RUN tar -xzf apache-activemq-5.15.6-bin.tar.gz
CMD ["apache-activemq-5.15.6/bin/activemq", "console"]



