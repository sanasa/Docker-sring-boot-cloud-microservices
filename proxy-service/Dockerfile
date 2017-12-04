FROM openjdk:8
ADD target/docker-proxy-spring-boot.jar docker-proxy-spring-boot.jar
EXPOSE 9999
ENTRYPOINT ["java","-jar","docker-proxy-spring-boot.jar"]