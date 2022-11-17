FROM adoptopenjdk/openjdk11:alpine
RUN apk add --no-cache curl && \
    curl -L https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v1.2.0/opentelemetry-javaagent-all.jar \
    -o /opt/otel-javaagent.jar
COPY /target/{{cookiecutter.baseName}}-0.0.1-SNAPSHOT-runner.jar /opt/app.jar
RUN adduser -D 1000
USER 1000
CMD java -javaagent:/opt/otel-javaagent.jar \
    -Dotel.resource.attributes="service.name=$APM_SERVICE,environment=$APM_ENVIRONMENT,com.splunk.signalfx.access_token=$SIGNALFX_TOKEN" \
    -jar /opt/app.jar
