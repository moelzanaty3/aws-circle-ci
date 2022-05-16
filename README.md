# Steps to configure CircleCI with AWS S3, RDS and Elastic Beanstalk

[![CircleCI](https://circleci.com/gh/moelzanaty3/react-aws-circle-ci/tree/main.svg?style=svg)](https://circleci.com/gh/moelzanaty3/react-aws-circle-ci/tree/main)

## CIRCLE CI

1. Create Circle CI Project
2. Setup Environment Variables

| Name                  |                         Value                         |
| --------------------- | :---------------------------------------------------: |
| AWS_REGION            |  The AWS region you used to provision RDS, S3 and EB  |
| AWS_ACCESS_KEY_ID      |                 Your AWS Access key ID               |
| AWS_SECRET_ACCESS_KEY |              Your AWS secret Access key               |
| AWS_S3_ENDPOINT       |             The url of the S3 hosted app.             |
| AWS_REGION            |  The AWS region you used to provision RDS, S3 and EB  |
| AWS_PROFILE           |                   Your AWS profile                    |
| AWS_BUCKET            | The name of the S3 bucket used to host the front end  |
| ----------------------|-------------------------------------------------------|
| POSTGRES_HOST         |         The url of the RDS database instance          |
| POSTGRES_DB           |                       postgres                        |
| POSTGRES_USERNAME     | The username specified when creating the RDS instance |
| POSTGRES_PASSWORD     | The password specified when creating the RDS instance |
| DB_PORT               |  The port of the RDS db instance (5432 for postgres)  |

## AWS

- Create IAM user with `AdministratorAccess`

- Configure the aws cli user with your terminal via `aws configure`

### Create S3 Bucket

- open terminal  and run the following to create s3 bucket

```bash
aws s3api create-bucket \
           --bucket zanaty-bucket-1 \
           --region us-east-1
```

- Set Bucket Policy for S3 Bucket

make sure u change `NAME_OF_YOUR_BUCKET` with your bucket name in my case will be `zanaty-bucket-1`

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

- in your s3 bucket properties go to static website hosing and enable it as below image and save the changes

![images](./docs/images/s3-static-web-hosting.png)

- you should have a url for example `http://zanaty-bucket-1.s3-website-us-east-1.amazonaws.com/`

- now it's time to upload you static files and this can be by

```bash
aws s3 sync build/ s3://zanaty-bucket-1
```

> look for why `sync` not `cp` 'https://stackoverflow.com/a/64728207/6483379'

🐻 Delete all resource after you finish

```bash
aws s3 rb s3://zanaty-bucket-1 --force  
```
