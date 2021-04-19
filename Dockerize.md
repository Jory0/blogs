# Dockerize: Take an existing app and turn it into a docker image

Things to keep in mind:

- What dependencies are needed?
- What ports need to be exposed to reach the application (what is the application serving?)
- What are the commands you need to include in your Dockerfile?
- What are the commands you need to use to build the Image and Publish on your container repo?

(make note about using sudo vs adding user to docker group)

`docker build [location]` - This will read the Dockerfile and containerize the contents (can be a url to a remote git repo)

- `-t` tags the image

The `FROM` instruction indicates which base image you are using for your new image. Always use from official repos.

The `RUN` instruction will run commands within the image, creating a new layer on top of your base image.

The `COPY` instruction adds files from the _build context_ into the image. Also creating a new layer.

The `EXPOSE` instruction is purely documentation for which network port is being used by the application.

The `ENTRYPOINT` instruction specifies the default application to run when an container has been created from this image.

```
FROM alpine
RUN apk add --update nodejs nodejs-npm
COPY . /src
WORKDIR /src
RUN npm install
EXPOSE 8080
ENTRYPOINT ["node", "./app.js"]
```