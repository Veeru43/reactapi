# Use official node image as the base image
FROM node:14.16.0 as build

# Set the working directory
WORKDIR /usr/local/app

# Add the source code to app
COPY ./ /usr/local/app/

RUN npm config set strict-ssl false
# Install all the dependencies
RUN npm install
# RUN npm install -g@angular/cli
# Generate the build of the application
#RUN ng build
RUN npm run build:dev


# Stage 2: Serve app with nginx server



# Copy the build output to replace the default nginx contents.



#remove the code after building and moving to nginx
# RUN rm -rf /usr/local/app

# Use official nginx image as the base image
FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/* 
RUN rm -rf /etc/nginx/nginx.conf
COPY docker/dev/nginx.conf /etc/nginx/nginx.conf
COPY --from=build /usr/local/app/build/ /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

# Expose port 80
