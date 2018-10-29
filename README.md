# About this repository
For running codenize.tools on circleCI

[DockerImage](https://hub.docker.com/r/gunosy/circleci_codenize_tools/)
[![Docker Repository on Quay](https://quay.io/repository/saorio/circleci_codenize_tools/status "Docker Repository on Quay")](https://quay.io/repository/saorio/circleci_codenize_tools)

## How to Use for CircleCI

```
version: 2
jobs:
  build:
    docker:
      - image: gunosy/circleci_codenize_tools:latest
    working_directory: ~/<your-repository-name>
    environment:
      AWS_REGION: us-east-1
    steps:
      - checkout
      - run:
          name: miam dry-run
          command: |
            miam --dry-run --apply -f IAMfile --region ${AWS_REGION} --no-color --no-progress
      - deploy:
          name: miam deploy
          command: |
            if [ "${CIRCLE_BRANCH}" == "master" ]; then
              miam --apply -f IAMfile --region ${AWS_REGION} --no-color --no-progress
            fi
```

## Notice
CircleCI requires AWS permissions.
