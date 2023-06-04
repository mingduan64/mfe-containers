# 1. Build
FROM node:16-alpine3.18 AS build
WORKDIR /source
COPY package.json package.json
RUN npm install --force
ARG PUBLIC_URI
COPY . .
RUN npm run build

#2. Runtime
FROM nginx:mainline-alpine3.17-slim
COPY --from=build /source/dist /usr/share/nginx/html/
EXPOSE 80