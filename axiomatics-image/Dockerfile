FROM eclipse-temurin:17-jre

LABEL author="david.brossard@axiomatics.com"

ARG ADS_VER

ENV SRC_HOME=bin/access-decision-service
ENV ADS_HOME=/usr/share/ads
RUN echo $ADS_VER
ENV ADS_VER=$ADS_VER
RUN echo ENV ADS_VER: ${ADS_VER}

WORKDIR ${ADS_HOME}

COPY ${SRC_HOME}/access-decision-service-${ADS_VER}.jar ${ADS_HOME}/ads.jar
COPY ${SRC_HOME}/lib/http*.jar ${ADS_HOME}/lib/
COPY ${SRC_HOME}/lib/parser*.jar ${ADS_HOME}/lib/

COPY ads_deployment.yaml ${ADS_HOME}/conf/
COPY licenses/axiomatics_PDP.license ${ADS_HOME}/conf/

ENTRYPOINT $JAVA_HOME/bin/java -cp "./ads.jar:./lib/*" com.axiomatics.ads.App server conf/ads_deployment.yaml