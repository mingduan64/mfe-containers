# 1. Build each micro front ends
FROM node:17-alpine AS build-container
WORKDIR /source
COPY ./container/package.json package.json
RUN npm install --force
COPY ./container .
ARG CONTAINER_PUBLIC_URI=""
ARG MARKETING_PUBLIC_URI
ARG AUTH_PUBLIC_URI
ARG DASHBOARD_PUBLIC_URI
ARG PUBLIC_URI=${CONTAINER_PUBLIC_URI}
ARG MARKETING_URI=${MARKETING_PUBLIC_URI}
ARG AUTH_URI=${AUTH_PUBLIC_URI}
ARG DASHBOARD_URI=${DASHBOARD_PUBLIC_URI}
RUN npm run build

FROM node:17-alpine AS build-marketing
WORKDIR /source
COPY ./marketing/package.json package.json
RUN npm install --force
COPY ./marketing .
ARG MARKETING_PUBLIC_URI
ARG PUBLIC_URI=${MARKETING_PUBLIC_URI}
RUN npm run build

FROM node:17-alpine AS build-auth
WORKDIR /source
COPY ./auth/package.json package.json
RUN npm install --force
COPY ./auth .
ARG AUTH_PUBLIC_URI
ARG PUBLIC_URI=${AUTH_PUBLIC_URI}
RUN npm run build

FROM node:14-alpine AS build-dashboard
WORKDIR /source
RUN apk add python3 && apk add make && apk add g++
ARG DASHBOARD_PUBLIC_URI
ARG PUBLIC_URI=${DASHBOARD_PUBLIC_URI}
COPY ./dashboard .
RUN npm install --force && npm run build

#2. Runtime
FROM  nginx:mainline-alpine3.17-slim
ARG CONTAINER_PUBLIC_URI
ARG MARKETING_PUBLIC_URI
ARG AUTH_PUBLIC_URI
ARG DASHBOARD_PUBLIC_URI
COPY --from=build-container /source/dist /usr/share/nginx/html/${CONTAINER_PUBLIC_URI}
COPY --from=build-auth      /source/dist /usr/share/nginx/html/${AUTH_PUBLIC_URI}
COPY --from=build-marketing /source/dist /usr/share/nginx/html/${MARKETING_PUBLIC_URI}
COPY --from=build-dashboard /source/dist /usr/share/nginx/html/${DASHBOARD_PUBLIC_URI}
EXPOSE 80
