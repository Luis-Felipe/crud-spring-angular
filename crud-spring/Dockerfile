##############################
# BUILD                      #
##############################
FROM maven:3.9.7-eclipse-temurin-22-alpine as build

WORKDIR /crud-spring

COPY pom.xml .
COPY src ./src
#COPY . .

RUN mvn clean package -DskipTests

##############################
# PRODUCTION                 #
##############################
FROM openjdk:22-rc as production

WORKDIR /crud-spring

COPY --from=build /crud-spring/target/crud-spring-0.0.1-SNAPSHOT.jar /crud-spring/app.jar

RUN ls -la /crud-spring/app.jar

# Use uma variável de ambiente para definir o perfil ativo
ENV SPRING_PROFILES_ACTIVE=dev


ENTRYPOINT ["java","-jar","/crud-spring/app.jar"]
