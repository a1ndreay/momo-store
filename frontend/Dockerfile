FROM node:16.20.0-alpine3.18 AS build
WORKDIR /app
COPY . .
RUN npm install
ARG NODE_ENV=production VUE_APP_API_URL=http://backend-momo-store:8081
RUN npm run build

FROM node:16.20.0-alpine3.18
WORKDIR /app
COPY --from=build /app .
EXPOSE 8080
ENTRYPOINT ["npm", "run", "serve"]
