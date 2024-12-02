# Stage1: Build wiuth nginx
# use node v20 as base image
FROM node:20-alpine as build

# set cyrrent working directory
WORKDIR /app/frontend

# copy package.json and package-lock.json to the working directory
COPY package*.json ./

# install dependencies
RUN npm install

# copy remaining files 
COPY . .

ARG VITE_API_URL

ENV VITE_API_URL=$VITE_API_URL

RUN npm run build

# Stage 2: serve the frontend with nginx

FROM  nginx:alpine 

COPY --from=build /app/frontend/dist /usr/share/nginx/html

# COPY nginx.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]