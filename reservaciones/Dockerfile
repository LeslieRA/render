# --- ETAPA 1: CONSTRUCCIÓN (BUILD) ---
# Usamos una imagen de Java 17 para compilar
FROM eclipse-temurin:17-jdk-alpine as build

# Creamos una carpeta de trabajo
WORKDIR /app

# Copiamos todos tus archivos del proyecto a la imagen
COPY . .

# Damos permisos de ejecución al instalador de Maven (por si acaso)
RUN chmod +x mvnw

# Ejecutamos el comando para compilar (crear el .jar)
RUN ./mvnw clean package -DskipTests

# --- ETAPA 2: EJECUCIÓN (RUN) ---
# Usamos una imagen limpia y ligera para correr la app
FROM eclipse-temurin:17-jdk-alpine

# Carpeta de trabajo
WORKDIR /app

# Copiamos SOLO el archivo .jar creado en la etapa anterior
# (El asterisco *.jar sirve para que no importe si cambia la versión)
COPY --from=build /app/target/*.jar app.jar

# Le decimos a Docker que este servicio usa el puerto 8080
EXPOSE 8080

# Comando para iniciar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]