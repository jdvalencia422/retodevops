FROM node:lts-alpine

# Create app directory
WORKDIR /usr/src/app

#COPY app files to container
COPY . .

#Create user devops
RUN adduser devops --disabled-password
RUN npm install
RUN npm install -g @angular/cli

#Run with user devops
USER devops

#Expose app port
EXPOSE 4200
CMD ng serve --host 0.0.0.0
