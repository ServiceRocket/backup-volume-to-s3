# servicerocket/backup-volume-to-s3

> Backup a single path in the instance to specified S3 path


## How frequent will it run?

Daily at midnight

## What is the backup strategy?

Duply is used. Basically, it will generate incremental tarball to the specified target.
Generally, it will generate full backup on the first time and next backups will be incremental.
For this project, it's configured to use S3 bucket.

## Getting Started

- Assume that there is an existing docker container running and mount `/data/` volume.
- Backup operation can be run via:

      docker run --name backup -d \
          -e SOURCE="/data" \
          -e TARGET="s3://s3-us-west-2.amazonaws.com/bucket-name/path/to/backup" \
          -e TARGET_USER="aws_access_key" \
          -e TARGET_PASS="aws_secret_access_key" \
          servicerocket/backup-volume-to-s3

## Modifying Backup Behaviour

Override duply properties file into `/root/.duply/backupconfiguration/conf` using Docker volume mount.