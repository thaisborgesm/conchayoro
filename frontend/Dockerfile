FROM node:18-alpine AS build-stage

WORKDIR /app

COPY package*.json ./
COPY . ./

RUN npm install
RUN npm run build
RUN apt-get update && apt-get remove python3-pip -y && \
    python -m ensurepip --upgrade && \
    python -m pip install --upgrade pip

FROM nginx:1.19.3-alpine AS production-stage

COPY --from=build-stage /app/out /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
