FROM node:lts-alpine

# Create app directory
WORKDIR /usr/src/app

#COPY app files to container
COPY . .

#Create user devops
RUN adduser devops --disabled-password

#Run with user devops
USER devops

#Expose app port
EXPOSE 3000
CMD [ "node", "app.js" ]
