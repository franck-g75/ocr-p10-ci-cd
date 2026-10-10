FROM node:latest as build

WORKDIR /usr/local/app
COPY ./ /usr/local/app/

# Install all the dependencies (au lieu de RUN yarn qui est inconnu dans le conteneur)
RUN npm ci --ignore-scripts
#Omitting "--ignore-scripts" allows lifecycle scripts to run during package installation.

# Generate the build of the application
RUN npm run build
 
FROM nginx:latest as production

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html

EXPOSE 80