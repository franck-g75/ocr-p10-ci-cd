#Build le projet
FROM maven:3.6.3-jdk-11-slim AS build
RUN mkdir -p /workspace
WORKDIR /workspace
COPY pom.xml /workspace
COPY src /workspace/src
RUN mvn -B -f pom.xml clean package -DskipTests

#Demarrage du projet
FROM eclipse-temurin:11-jdk
#The "eclipse-temurin" image runs with "root" as the default user. Make sure it is safe here.
#ARG JAR_FILE=/workspace/target/*.jar
RUN mkdir /home/nobody
WORKDIR /home/nobody
#COPY ${JAR_FILE} app.jar
COPY --from=build /workspace/target/*.jar app.jar
USER 65534

EXPOSE 8080

#Demarrer au lancement du conteneur
ENTRYPOINT ["java", "-jar","app.jar"]
