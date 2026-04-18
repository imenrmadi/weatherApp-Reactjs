FROM node:20 as build
WORKDIR /app

# Copier SEULEMENT package.json d'abord
COPY package*.json ./
RUN npm ci

# Ensuite copier le reste
COPY . .
ENV NODE_OPTIONS=--openssl-legacy-provider
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80