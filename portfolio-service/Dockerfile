FROM java:8-jre
ENV VERTICLE_FILE portfolio-service-1.0-SNAPSHOT-fat.jar
ENV VERTICLE_HOME /usr/verticles
EXPOSE 8080
COPY target/$VERTICLE_FILE $VERTICLE_HOME/
COPY $VERTICLE_CONFIG $VERTICLE_HOME/
RUN chmod 777 $VERTICLE_HOME
WORKDIR $VERTICLE_HOME
ENTRYPOINT ["sh", "-c"]
CMD ["java -jar $VERTICLE_FILE -conf config.json -cp . -cluster -Dvertx.metrics.options.enabled=true -Dvertx.metrics.options.jmxEnabled=true -Dvertx.disableFileCPResolving=true"]

