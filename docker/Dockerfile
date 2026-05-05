FROM node:20-alpine AS build

WORKDIR /app

COPY package*.json ./

# ✅ Cache npm persistant entre les builds (BuildKit)
RUN --mount=type=cache,target=/root/.npm \
    npm ci --prefer-offline

COPY . .

ENV NODE_OPTIONS=--openssl-legacy-provider

RUN npm run build

# ─────────────────────────
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
