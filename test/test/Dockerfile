# Utilisation d'une image légère basé sur alpine.
FROM node:15-alpine3.10 as builder

# Ensemble des commandes pour installation une application node en production
COPY package.json package-lock.json ./
RUN npm install --only=prod && mkdir /react-frontend && mv ./node_modules ./react-frontend
WORKDIR /react-frontend
COPY . .
RUN npm run build

#FROM nginx:1.19.6-alpine 
FROM nginxinc/nginx-unprivileged
COPY --from=builder /react-frontend/build /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx/nginx.conf /etc/nginx/conf.d
EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
