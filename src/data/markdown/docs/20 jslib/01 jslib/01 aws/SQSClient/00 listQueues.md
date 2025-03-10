---
title: 'SQSClient.listQueues()'
description: "SQSClient.listQueues retrieves a list of available Amazon SQS queues"
excerpt: "SQSClient.listQueues retrieves a list of available Amazon SQS queues"
---

`SQSClient.listQueues(options)` retrieves a list of available Amazon Simple Queue Service (SQS) queues.

### Parameters

| Name          | Type              | Description                                                                                                                                                                  |
| :------------ | :---------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `options`     | object (optional) | Options for the request. Accepted properties are: `queueNamePrefix` (optional string) setting the prefix filter for the returned queue list, `maxResults` (optional number) setting the maximum number of results to include in the response (1 <= `maxResults` <= 1000>), and `nextToken` (optional string) setting the pagination token to request the next set of results. |

### Returns

| Type                                                        | Description                                                               |
| :---------------------------------------------------------- | :------------------------------------------------------------------------ |
| `object` | An object with an `urls` property containing an array of queue URLs, and an optional `nextToken` containing a pagination token to include in the next request when relevant. |

### Example

<CodeGroup labels={[]}>

```javascript
import exec from 'k6/execution'

import { AWSConfig, SQSClient } from 'https://jslib.k6.io/aws/0.8.1/sqs.js'

const awsConfig = new AWSConfig({
    region: __ENV.AWS_REGION,
    accessKeyId: __ENV.AWS_ACCESS_KEY_ID,
    secretAccessKey: __ENV.AWS_SECRET_ACCESS_KEY,
    sessionToken: __ENV.AWS_SESSION_TOKEN,
})

const sqs = new SQSClient(awsConfig)
const testQueue = 'https://sqs.us-east-1.amazonaws.com/000000000/test-queue'

export default function () {
    // List all queues in the AWS account
    const queuesResponse = sqs.listQueues()

    // If our test queue does not exist, abort the execution.
    if (queuesResponse.queueUrls.filter((q) => q === testQueue).length == 0) {
        exec.test.abort()
    }

    // Send message to test queue
    sqs.sendMessage(testQueue, JSON.stringify({value: '123'}));
}
```

</CodeGroup>