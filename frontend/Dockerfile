FROM node:18-alpine as build-stage

WORKDIR /app

# Instala dependências de build como make, python e g++
RUN apk add --no-cache python3 make g++

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

FROM nginx:1.19.3-alpine as production-stage

COPY --from=build-stage /app/.next/server/app /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
