# Steps

## CIRCLE CI

1. Create Circle CI Project
2. Setup Environment Variables

| Name                  |                         Value                         |
| --------------------- | :---------------------------------------------------: |
| AWS_REGION            |  The AWS region you used to provision RDS, S3 and EB  |
| AWS_ACCESS_KEY_ID      |                 Your AWS Access key ID               |
| AWS_SECRET_ACCESS_KEY |              Your AWS secret Access key               |

## AWS

1. Create IAM user with `AmazonS3FullAccess`

2. Create S3 Bucket

3. Set Bucket Policy for S3 Bucket

make sure u change `NAME_OF_YOUR_BUCKET` with your bucket name

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::NAME_OF_YOUR_BUCKET/*"
            ]
        }
    ]
}
```
