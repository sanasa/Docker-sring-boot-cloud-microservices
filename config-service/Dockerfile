FROM openjdk:8
ADD target/docker-config-spring-boot.jar docker-config-spring-boot.jar
EXPOSE 8888
ENTRYPOINT ["java","-jar","docker-config-spring-boot.jar"]