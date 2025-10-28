# ======= BUILD STAGE =======
FROM eclipse-temurin:21-jdk-alpine AS build
WORKDIR /app

# Installe Maven
RUN apk add --no-cache maven

# Copie les fichiers nécessaires
COPY pom.xml .
COPY src ./src

# Compile et package l'application (sans les tests)
RUN mvn clean package -DskipTests

# ======= RUNTIME STAGE =======
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app

# Copie le JAR depuis la phase précédente
COPY --from=build /app/target/*.jar app.jar

# Expose le port utilisé par Spring Boot
EXPOSE 8080

# Commande de démarrage
ENTRYPOINT ["java", "-jar", "app.jar"]
