
FROM node

RUN npm install -g @angular/cli

WORKDIR /app
COPY package.json /app/
COPY package-lock.json /app/
RUN npm install

COPY . /app/

RUN ng build

# TODO need to have a container with chrome in it to run tests
#RUN ng test

EXPOSE 4200
CMD ng serve --host 0.0.0.0 --port 80