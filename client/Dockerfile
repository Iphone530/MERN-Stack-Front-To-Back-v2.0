FROM node:alpine as builder

RUN mkdir -p /project
WORKDIR '/project'

COPY ./package*.json ./
RUN npm install

COPY . ./

RUN npm run build

FROM nginx

RUN apt update && apt upgrade && \
  apt install -y bash vim less curl iputils-ping dnsutils

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /project/build /usr/share/nginx/html