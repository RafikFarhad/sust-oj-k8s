# SUST Online Judge

This repository contains all _Kubernetes_ configuration files for deploying out [SUST Online Judge](https://beta.sustcseoj.com).

_We are in still beta version of this release. Although our [alpha](https://alpha.sustcseoj.com) version is running as a production version for internal use inside the university_

Our project is broken down on several microservices after we delivered the alpha version to the university. And the current version is a voluntary effort from the creators and backers.

## Creators

- Rafik Farhad [@RafikFarhad](https://github.com/RafikFarhad)
- Talat Mursalin [@talatmursalin](https://github.com/talatmursalin)

## Technologies

Begining of this project we started with `Laravel 5` as our web end, `Python2.7` for our judging system. For the time being, we introduced more technology as we felt necessary for this project. Currently, the project is broken down with these following micro-services.

| Repository                                                                                    | Technology    | Role                                   |
| --------------------------------------------------------------------------------------------- | ------------- | -------------------------------------- |
| [judgeMod](https://github.com/talatmursalin/judgeMod)                                         | Python3       | Judging and Sandboxing                 |
| [masterCODE](https://github.com/RafikFarhad/masterCODE)                                       | Laravel 7     | Main API Backend                       |
| [doCODE](https://github.com/RafikFarhad/doCODE)                                               | NuxtJS        | Contestant Frontend                    |
| [subCODE](https://github.com/RafikFarhad/subCODE)                                             | Laravel 7     | Judge Interface                        |
| [liveCODE](https://github.com/RafikFarhad/liveCODE)                                           | NodeJS        | Real time notification provider via WS |
| -                                                                                             | Minio         | S3 Complient Storage Service           |
| -                                                                                             | MySQL         | Database Service                       |
| -                                                                                             | RabbitMQ      | Inter-service messaging service        |
| -                                                                                             | Redis DB      | Caching Service                        |
|                                                                                               | ELK Stack     | Logging                                |
| [push-to-gcr-github-action](https://github.com/marketplace/actions/push-to-gcr-github-action) | Github Action | CI/CD                                  |

_Currently, our repositories are not public. We will make them public as soon as we are ready to release and tag the projects with proper license_

## Deployments

We use continuous deployment process in our project. Everytime we released a version with a `git tag`, the `github-action` automatically builds an appropriate docker image and pushes the image in docker registry. Currently, we are using `Google Cloud Registry`. For this, we released a generic [github-action](https://github.com/marketplace/actions/push-to-gcr-github-action) in the marketplace to make this step automated.

## Development

In development, we use `docker-compose` like all others. You can find the `docker-compose` configs file in this repository: [sust-oj-compose](https://github.com/RafikFarhad/sust-oj-compose)
