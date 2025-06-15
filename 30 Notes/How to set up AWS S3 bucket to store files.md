---
created: 2024-05-12 12:10 
modified: Sunday 12th May 2024 12:10:17
alias: 
---
up:: 
tags:: #s3-bucket #aws 
type:: #notes/how-to
links::
## How to set up AWS S3 bucket to store files?
### Create AWS user
1. Go to [AWS Console](https://us-east-1.console.aws.amazon.com/console/home?region=us-east-1)
2. Search **IAM** 
	Go to Access management -> [Users](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/users)
3. Select **Create user** button
	1. Set username (ex. twitter-fullstack-s3)
	2. Set permissions
		Permissions options ->**Attach Policies Directly**
		Permission policies -> search S3 ->
			**AmazonS3FullAccess**
	3. Review and **create user**

### Get access keys
1. Go to [IAM User -> Security credentials](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/users/details/twitter-fullstack?section=security_credentials)
2. Select **create access key**
	use case- **Command Line Interface**
3. Save the AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY

### Create AWS S3 bucket
1. Go to [S3 Bucket Console](https://us-east-1.console.aws.amazon.com/s3/home?region=us-east-1)
2. Set bucket name ex. "twitter-fullstack"
3.  In the **"Block Public Access settings"** section, you can choose allow public access to your bucket and its objects.
4. Review and create the bucket
``
### Setting up S3 Bucket Policy
1. Go to [S3 Bucket Console](https://us-east-1.console.aws.amazon.com/s3/home?region=us-east-1)
2. Select your bucket -> Permissions
3. Edit the bucket policy and paste the policy below
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject",
                "s3:GetObjectVersion"
            ],
            "Resource": "arn:aws:s3:::twitter-fullstack/*"
        }
    ]
}
```
4. Configure cross-origin resource sharing (CORS)
	```
	[
	  {
	    "AllowedHeaders": [
	      "*"
	    ],
	    "AllowedMethods": [
	      "GET",
	      "HEAD",
	      "PUT"
	    ],
	    "AllowedOrigins": [
	      "http://localhost:3000"
	    ],
	    "ExposeHeaders": [],
	    "MaxAgeSeconds": 3000
	  }
	]
	```

[[How to upload images to S3 bucket with a presignedURL]]

**Sources**

