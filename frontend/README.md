# Deploying the frontend to S3

(unfinished and very rough - I don't like the hacky manual upload part in 4, I'm still aiming to replace that with a one-liner npm command using the aws cli, just haven't done it yet.. feel free to be faster and file a pull request with that :-) )

In general:

1. Create a bucket in S3 that can serve webpages
   
2. make sure it has the proper policy attached and contens are world readable:

Bucket policy:
```
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
                "arn:aws:s3:::timetrack-test/*"
            ]
        }
    ]
}
```

3. Build the frontend

```
~/your-application/frontend$ npm run build:production
```

4. copy the contents of ~/your-application/frontend/build to your S3 website serving bucket from step 2.

