# apollo-client-aws-ni
Provides a network interface for the official Apollo client in order to allow connection to graphql server protected behind a Amazon AWS API Gateway.

## Installation
```npm install apollo-client-aws-ni --save```

## Basic usage :
```
import { ApolloClient } from 'apollo-client';
import { AwsApiGwClient, AwsApiGwNetworkInterface } from "apollo-client-aws-ni/api-gw-connector";
declare var apigClientFactory: any; // being the AWS API GW generated SDK root object (to be imported in main html file)

var apigClient = apigClientFactory.newClient({ ... });
var clientSet = true;

const awsApiGwClient: AwsApiGwClient = {
  isAuthenticated(){
    return clientSet;
  },
  authenticationExpired(){
    clientSet = false;
  },
  graphqlPost(param, body, extra) {
    return apigClient.testPost(param, body, extra);
  }
}

const networkInterface: any = new AwsApiGwNetworkInterface(awsApiGwClient);
const client: ApolloClient = new ApolloClient({
  networkInterface: networkInterface,
});
```

## Related blog post
Coming soon...
