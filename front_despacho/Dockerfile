# Etapa 1: Compilación (Build)
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
# Ojo aquí: cambia "npm run build" si tu proyecto usa otro comando, 
# y asegúrate de que la carpeta resultante sea "dist" o "build".
RUN npm run build 

# Etapa 2: Producción (Run) - Imagen Oficial sin privilegios
FROM nginxinc/nginx-unprivileged:alpine

# Copiamos los archivos compilados desde la etapa 1
# Si tu frontend genera una carpeta "build" en lugar de "dist", cámbialo en la línea de abajo:
COPY --from=builder /app/dist /usr/share/nginx/html

# Esta imagen escucha por defecto en el puerto 8080 sin necesidad de ser root
EXPOSE 8080
