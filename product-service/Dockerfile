FROM openjdk:8
ADD target/docker-product-spring-boot.jar docker-product-spring-boot.jar
EXPOSE 8081
ENTRYPOINT ["java","-jar","docker-product-spring-boot.jar"]