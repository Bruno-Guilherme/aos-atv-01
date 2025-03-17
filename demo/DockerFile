#
# Build stage
#
FROM maven:3.9-eclipse-temurin-21-alpine AS build
COPY . .
RUN mvn clean package -DskipTests

#
# Package stage
#
FROM eclipse-temurin:21-jre-alpine

# Cria um usuário não privilegiado
RUN adduser -D appuser
USER appuser

# Copia o JAR gerado no estágio de build
COPY --from=build /target/*.jar app.jar

# Expõe a porta 8080
EXPOSE 8080

# Comando de execução
ENTRYPOINT ["java","-jar","app.jar"]