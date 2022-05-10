# sls-nodejs-ts-aws-example


This project has been generated using the `aws-nodejs-typescript` template from the [Serverless framework](https://www.serverless.com/).

For detailed instructions, please refer to the [documentation](https://www.serverless.com/framework/docs/providers/aws/).

This repository contains a VSCode Remote Container Setup for developing NodeJS based AWS Lambda functions using the Serverless Framework.

## Visual Studio Code - Remote Container Usage

> [Official Documentation](https://code.visualstudio.com/docs/remote/containers)

> _Note: Once you meet the prerequisites, you can run **ANY** Visual Studio Code Remote Container, which provides a Docker based development environment ensuring a consistent and reliable set of tooling needed to interact and execute a repository codebase_

### Prerequisites:

1. macOS, Windows, Linux -- [System Requirements](https://code.visualstudio.com/docs/remote/containers#_system-requirements)
2. Docker - [Documentation](https://code.visualstudio.com/docs/remote/containers#_installation)
3. Visual Studio Code - [Official Site](https://code.visualstudio.com/)
4. Remote - Containers _Visual Studio Code extension_ - [Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

#### Environment Variables

The remote container honors the following environment variables set in the .devcontainer/.env

> _Note: You can copy the [.devcontainer/.env.template](.devcontainer/.env.template) file to .devcontainer/.env and supply the following variables_

##### AWS

- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- AWS_REGION - (optional - defaults to us-east-2)

> _Note: Changes to variables in .env after the container is running will require the Remote Container to be restarted_

#### Developer Configuration

To initialize the environment, once the repository is opened in the Remote Container, open a Terminal and type:

`yarn`

### Usage & Things you can do

#### package.json Scripts

There are some predefined scripts in package.json that can be used to simplify common tasks.

- `yarn start` - runs the functions locally using the AWS configuration
- `yarn deploy` - deploys the functions to AWS
- `yarn undeploy` - undeploys the functions from AWS

#### Test the service

This template contains a single lambda function triggered by an HTTP request made on the provisioned API Gateway REST API `/hello` route with `POST` method. The request body must be provided as `application/json`. The body structure is tested by API Gateway against `src/functions/hello/schema.ts` JSON-Schema definition: it must contain the `name` property.

`yarn start`

Use the APIs from the provided [postman_collection.json](postman_collection.json)

#### Debugging - Local

All of the [package.json](package.json) scripts defined above can be run in a 'JavaScript Debug Terminal' which automatically attaches the debugger.

#### Project structure

The project code base is mainly located within the `src` folder. This folder is divided in:

- `functions` - containing code base and configuration for your lambda functions
- `libs` - containing shared code base between your lambdas

```
.
├── src
│   ├── functions               # Lambda configuration and source code folder
│   │   ├── hello
│   │   │   ├── handler.ts      # `Hello` lambda source code
│   │   │   ├── index.ts        # `Hello` lambda Serverless configuration
│   │   │   ├── mock.json       # `Hello` lambda input parameter, if any, for local invocation
│   │   │   └── schema.ts       # `Hello` lambda input event JSON-Schema
│   │   │
│   │   └── index.ts            # Import/export of all lambda configurations
│   │
│   └── libs                    # Lambda shared code
│       └── apiGateway.ts       # API Gateway specific helpers
│       └── handlerResolver.ts  # Sharable library for resolving lambda handlers
│       └── lambda.ts           # Lambda middleware
│
├── package.json
├── serverless.ts               # Serverless service file
├── tsconfig.json               # Typescript compiler configuration
├── tsconfig.paths.json         # Typescript paths
└── webpack.config.js           # Webpack configuration
```

### 3rd party libraries

- [json-schema-to-ts](https://github.com/ThomasAribart/json-schema-to-ts) - uses JSON-Schema definitions used by API Gateway for HTTP request validation to statically generate TypeScript types in your lambda's handler code base
- [middy](https://github.com/middyjs/middy) - middleware engine for Node.Js lambda. This template uses [http-json-body-parser](https://github.com/middyjs/middy/tree/master/packages/http-json-body-parser) to convert API Gateway `event.body` property, originally passed as a stringified JSON, to its corresponding parsed object
- [@serverless/typescript](https://github.com/serverless/typescript) - provides up-to-date TypeScript definitions for your `serverless.ts` service file

### Advanced usage

Any tsconfig.json can be used, but if you do, set the environment variable `TS_NODE_CONFIG` for building the application, eg `TS_NODE_CONFIG=./tsconfig.app.json npx serverless webpack`
