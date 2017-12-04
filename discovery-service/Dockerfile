FROM openjdk:8
ADD target/docker-discovery-spring-boot.jar docker-discovery-spring-boot.jar
RUN sh -c 'touch /docker-discovery-spring-boot.jar'
EXPOSE 8761
ENV JAVA_OPTS=""
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar docker-discovery-spring-boot.jar" ]