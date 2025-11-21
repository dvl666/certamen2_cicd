FROM node:14 AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

# Copiar el código del proyecto
COPY . .

# Compilar Angular para producción
RUN npm run build --prod

# Etapa 2: Servir con Nginx
FROM nginx:alpine

# Eliminar default.conf y colocar uno propio
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copiar los artefactos compilados desde la etapa builder
COPY --from=builder /app/dist/dragonballapp /usr/share/nginx/html

# Exponer el puerto 80
EXPOSE 80

# Iniciar nginx
CMD ["nginx", "-g", "daemon off;"]
