FROM node:18-alpine as build-stage

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

# Exibe as dependências instaladas e o Node.js/npm para garantir que tudo está correto
RUN node -v && npm -v && npm list

# Executa o build com mais verbosidade para capturar mais informações
RUN npm run build --verbose

FROM nginx:1.19.3-alpine as production-stage

COPY --from=build-stage /app/.next/server/app /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
