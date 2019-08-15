# AppSync2EventBridge

Send events via GraphQL to AWS Event Bridge:

AppSync GraphQL API -> Event Bridge -> AWS Lambda

## Build

To build this app, you need to be in thieroot folder. Then run the following:

```bash
npm install -g aws-cdk
npm install
npm run build
```

This will install the necessary CDK, then this example's dependencies, and then build your TypeScript files and your CloudFormation template.

## Deploy

Run `cdk deploy`. This will deploy / redeploy your Stack to your AWS Account.

After the deployment you will see the API's URL, which represents the url you can then use.

## Synthesize Cloudformation Template

To see the Cloudformation template generated by the CDK, run `cdk synth`, then check the output file in the "cdk.out" directory.

## The Component Structure

This Stack contains:

- a __GraphQL API__ with an API Key (Use with caution, each key is only valid for 7 days.)
- a __GraphQL Schema__ with Queries to get one and all items and two mutations to save and delete an item
- an __IAM Role__ that allows AppSync to invoke your Event Bus.
- an __AppSync DataSource__, connecting your API to Event Bus using a HTTP Resolver
- a __AppSync Resolver__ for a Mutation `putEvent` to send a custom event to Event Bridge
- a __Event Rule__ that listens for an event comming from AppSync and triggers a Lambda function
- a __Lambda__ for a function that just prints the event, you can confirm it's triggered by Event Bridge by checking the logs on CloudWatch.
