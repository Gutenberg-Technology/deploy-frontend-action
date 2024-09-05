# deploy-frontend-action

## Scenario

This Composite Action will run the following actions in AWS:

- Sync folder to S3
- Create CloudFront invalidation and run it

## Inputs

:warning: AWS credentials must be configured outside of this Composite.

The Composite Action takes as inputs the AWS' info such as S3 bucket name, S3 folder, CloudFrontID and the folder to upload.

See the [action.yml](action.yml) file for more details.


## Basic example

```yaml
name: deploy-frontend

on:
  push:

jobs:
  deploy_frontend:
    name: 'Deploy Frontend'
    runs-on: ubuntu-latest

    steps:
      - name: Configure AWS credentials
        id: aws-credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - uses: Gutenberg-Technology/deploy-frontend-action@v1.0.0
        with:
          folder-to-upload: /path/to/local/folder
          aws-region: us-east-1
          aws-cloudfront-distribution-id: QWERTYUIOP123456
          aws-bucket-name: my-bucket-name
          aws-bucket-folder: /path/to/s3/folder
```