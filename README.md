# Ada Admissions Landing Page #

## Deploying ##

### AWS Credentials ###

To deploy you will first need to have your AWS credentials configured.

You will need:
1. An AWS account (this is separate from your normal Amazon account)
  * You will probably want to create one for the [AWS Console](https://console.aws.amazon.com).
2. Access to the administrator account on [LastPass](https://lastpass.com) or the help of someone that does have these credentials.
3. To create `~/.aws/config`.  It should look like:

```config
[profile dev]
aws_access_key_id = AKIA...
aws_secret_access_key = ...

[profile prod]
aws_access_key_id = AKIA...
aws_secret_access_key = ...

[default]
region = us-west-2
```

You can use the same key for both the `dev` and `prod` sections.

4. You will to create `~/.aws/credentials`.  It should look like:
```config
[default]
aws_access_key_id = AKIA...
aws_secret_access_key = ...
```
These keys should also be the same as above.

### Development ###

Once you have your credentials deploying to dev is pretty simple:
```bash
$ ./deploy dev
```

### Production ###

Deploying to production is trickier.  First you will need to do the actual deploy:
```bash
$ ./deploy prod
```

Then you will need to use the [Cloudfront Console](https://console.aws.amazon.com/cloudfront) to create an "invalidation" to clear the cache.  Otherwise you will have to wait for the cache to expire.  (Which is 24 hours by default.)

To create the invalidation:

1. Log into the [Cloudfront Console](https://console.aws.amazon.com/cloudfront).
2. Click into the "Invalidations" tab.
3. Click "Create Invalidation" and put in `/` as the object path.

