#baselevel image
FROM node:14 as base 

#Setting the envirenment variable 
ENV INSTANA_AUTO_PROFILE true
WORKDIR /opt/serve
COPY package.json .
RUN npm install
COPY server.js .


 
#Get the distroless image with nodejs 14
FROM gcr.io/distroless/nodejs:14

#WORKDIR /opt/serve
#Copy the files from the base image to the distroless image
COPY --from=base /opt/serve .
#Expose the port 8080 for the application
EXPOSE 8080

#Run the server.js file
CMD ["server.js"]


