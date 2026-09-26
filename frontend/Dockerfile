# ── Stage 1: Build ── 
# Usamos una imagen de Node.js para instalar dependencias y compilar el código de React en archivos planos.
FROM node:20-alpine AS builder
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install --silent
COPY . .
RUN npm run build

# ── Stage 2: Serve with nginx ──
# Descartamos Node.js y usamos una imagen ligera de Nginx. 
# Copiamos los archivos resultantes de la primera etapa dentro de la carpeta que Nginx usa para servir páginas web.
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
