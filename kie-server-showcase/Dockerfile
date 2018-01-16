FROM jboss/kie-server:7.5.0.Final
MAINTAINER "Chery" "chinrui1016@163.com"

####### 环境变量 ############
# ENV KIE_SERVER_ID kie-server
ENV KIE_SERVER_LOCATION http://localhost:8080/kie-server/services/rest/server
ENV KIE_SERVER_USER kieserver
ENV KIE_SERVER_PWD kieserver1!
# ENV KIE_SERVER_CONTROLLER http://localhost:8080/kie-wb/rest/controller
ENV KIE_SERVER_CONTROLLER_USER admin
ENV KIE_SERVER_CONTROLLER_PWD admin
ENV KIE_MAVEN_REPO http://localhost:8080/kie-wb/maven2
ENV KIE_MAVEN_REPO_USER admin
ENV KIE_MAVEN_REPO_PASSWORD admin
ENV JAVA_OPTS -Xms256m -Xmx512m -Djava.net.preferIPv4Stack=true -Dfile.encoding=UTF-8

####### Drools KIE Server 常规配置 ############
RUN mkdir -p $HOME/.m2
ADD etc/standalone-full-kie-server.xml $JBOSS_HOME/standalone/configuration/standalone-full-kie-server.xml
ADD etc/kie-server-users.properties $JBOSS_HOME/standalone/configuration/kie-server-users.properties
ADD etc/kie-server-roles.properties $JBOSS_HOME/standalone/configuration/kie-server-roles.properties
ADD etc/start_kie-server.sh $JBOSS_HOME/bin/start_kie-server.sh
ADD etc/settings.xml $JBOSS_HOME/../.m2/settings.xml

# 修改配置文件的归属，由原先的 root 用户分配给 jboss 用户 
USER root
RUN chown jboss:jboss $JBOSS_HOME/standalone/configuration/standalone-full-kie-server.xml && \
chown jboss:jboss $JBOSS_HOME/standalone/configuration/kie-server-users.properties && \
chown jboss:jboss $JBOSS_HOME/standalone/configuration/kie-server-roles.properties && \
chown jboss:jboss $JBOSS_HOME/bin/start_kie-server.sh && \
chown jboss:jboss $JBOSS_HOME/../.m2/settings.xml && \
chmod 755 $JBOSS_HOME/bin/start_kie-server.sh

# 切换到用户 jboss 
USER jboss

####### 启动 KIE-SERVER ############
WORKDIR $JBOSS_HOME/bin/
CMD ["./start_kie-server.sh"]
