FROM sebp/elk:630
MAINTAINER Artsiom Shmanouski <hav3y0u@gmail.com>
RUN apt-get update -qq && apt-get install -qqy \
    autossh \
    supervisor \
    htop \
    nano \
    tzdata

#Install JDBC plugin for logstash
WORKDIR ${LOGSTASH_HOME}
RUN gosu logstash bin/logstash-plugin install logstash-input-jdbc

ADD https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.7.22.tar.gz /tmp/
RUN tar -zxvf /tmp/mysql-connector-java-5.7.22.tar.gz -C /root/ \
  && rm /tmp/mysql-connector-java-5.7.22.tar.gz

# Change security entropy
RUN cat /root/app/java.security >> /etc/java-8-openjdk/security/java.security

#CMD that launch ELK stack and start all services
CMD ["/usr/local/bin/start.sh"]