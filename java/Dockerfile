# Build stage
FROM eclipse-temurin:21-jdk-alpine as build
WORKDIR /app

# Copiar mvnw y .mvn
COPY .mvn/ .mvn/
COPY mvnw pom.xml ./

# Dar permisos de ejecución a mvnw
RUN chmod +x mvnw

# Descargar dependencias
RUN ./mvnw dependency:go-offline

# Copiar el código fuente
COPY src ./src

# Compilar la aplicación
RUN ./mvnw clean package -DskipTests

# Runtime stage
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=build /app/target/java-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]