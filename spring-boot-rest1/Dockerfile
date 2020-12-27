FROM adoptopenjdk/openjdk11:alpine-jre
EXPOSE 8080
ADD /target/spring-boot-rest1.jar spring-boot-rest1.jar
ENTRYPOINT ["java","-jar","spring-boot-rest1.jar"]
