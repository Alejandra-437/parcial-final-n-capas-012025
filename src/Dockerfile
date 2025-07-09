# Etapa de construcción
FROM maven:3.9.6-eclipse-temurin-17 AS builder
WORKDIR /workspace

# Copiar pom.xml y descargar dependencias
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copiar el código fuente
COPY src ./src

# Construir el JAR (sin ejecutar pruebas)
RUN mvn clean package -DskipTests

# Etapa de ejecución
FROM eclipse-temurin:17-jdk-alpine
WORKDIR /app
EXPOSE 8080

# Copiar el JAR generado
COPY --from=builder /workspace/target/*.jar app.jar

# Ejecutar la app
ENTRYPOINT ["java", "-jar", "app.jar"]