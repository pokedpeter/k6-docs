---
title: 'S3Client.createMultipartUpload(bucketName, objectKey)'
description: 'S3Client.createMultipartUpload creates a multipart upload for an object key to a bucket'
excerpt: 'S3Client.createMultipartUpload creates a multipart upload to a bucket'
---

`S3Client.createMultipartUpload` creates a new multipart upload for a given an object key in a bucket.

| Parameter  | Type                  | Description                                  |
| :--------- | :-------------------- | :------------------------------------------- |
| bucketName | string                | Name of the bucket to upload the object to.  |
| objectKey  | string                | Name of the uploaded object.                 |

### Returns

| Type                                                                     | Description                                                                                                       |
| :----------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------- |
| [S3MultipartUpload](/javascript-api/jslib/aws/s3client/s3multipartupload) | An [S3MultipartUpload](/javascript-api/jslib/aws/s3client/s3multipartupload) representing a S3 Multipart Upload. |

### Example

<CodeGroup labels={[]}>

```javascript
import { AWSConfig, S3Client } from 'https://jslib.k6.io/aws/0.8.1/s3.js';

const awsConfig = new AWSConfig({
    region: __ENV.AWS_REGION,
    accessKeyId: __ENV.AWS_ACCESS_KEY_ID,
    secretAccessKey: __ENV.AWS_SECRET_ACCESS_KEY,
    sessionToken: __ENV.AWS_SESSION_TOKEN,
});

const s3 = new S3Client(awsConfig);

const testBucketName = 'test-jslib-aws';
const testFileKey = 'multipart.txt';

export default function () {
    // Initialize a multipart upload
    const multipartUpload = s3.createMultipartUpload(testBucketName, testFileKey);

    // Abort multipart upload
    s3.abortMultipartUpload(testBucketName, testFileKey, multipartUpload.uploadId);
}
```

_A k6 script that will create a multipart upload to an S3 bucket_

</CodeGroup>