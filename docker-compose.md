# How to write `docker-compose`

In visual code pressing `⌃Space` suggest valid compose directives.
- Precondition : Install `Docker` extension.
- Example :  ![ref](https://code.visualstudio.com/assets/docs/azure/docker/dockercomposeintellisense.png)

To use docker-compose we have to define `docker-compose.yml` file.

It's style is YAML.

## Docker compose for Running Tests
- See [docker-compose.yml](./react-app/docker-compose.yml)
  - `tests` directive shows how to run test `react-app`
  - `docker-compose up --build` to build add service.


## Docker attach
- `docker attach <container ID>`
  - ex) `docker attach react-app_tests_1`
  - Create additional container and attach to existing container.
  - 
- But in `react-app` case `npm` create subprocess(`start.js`) and we can't directly attach to it.