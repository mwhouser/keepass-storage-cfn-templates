keepass-storage-cfn-templates
=============================

This repository contains CloudFormation templates for storing [KeePass](https://keepass.info/) databases.

# keeanywhere-storage.yaml

This template is for the [KeeAnywhere](https://keeanywhere.de/) plugin.

## Resources Created

### S3 buckets

One S3 bucket will be created. 

* All public access to the bucket is intentionally blocked.
* Default AES256 encrypt-at-rest is enabled.

The bucket has a bucket policy attached to it. The policy enforces any access to the bucket uses SSL/HTTPS. This prevents plaintext HTTP access and ensures all transport (in and out) is encrypted.

### IAM users

One IAM user will be created.

* Access to the S3 bucket is permitted per the IAM policy at https://keeanywhere.de/use/faq

## Instructions

1. Open the CloudFormation management console in your desired region.
2. Create a new CloudFormation stack, using `keeanywhere-storage.yaml` as the template file.
3. When the stack is complete, make note of the following from the stack's `Outputs`:
    * The S3 bucket created
    * The IAM user
4. Navigate to the created IAM user and create an access key & secret pair. Copy/Paste the pair into KeeAnywhere.
5. Start Loading and saving your KeePass databases to the created bucket.

## Additional Notes

You should rotate your access keys regularly (for example, every 30 days).

If you need to create a second user to access the same bucket, simply copy & paste the entire `KeePassUser1` resource as a new resource (eg. `KeePassUser2`) and update your existing stack.
