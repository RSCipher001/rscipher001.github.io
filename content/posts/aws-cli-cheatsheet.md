---
title: "AWS Cli Cheatsheet"
date: 2019-12-19T00:02:00+05:30
description: "AWS Cli cheatsheet can be used as an reference to get job done on aws using command prompt"
tags: [aws, s3, cloud]
category: [AWS, Cloud]
---

This page contains most commonly used aws cli cheatsheet.

## Create a bucket
```bash
aws s3 mb s3://bucket-name
```

## List all bucket
```bash
aws s3 ls
```

## List files in a bucket
```bash
aws s3 ls s3://bucket-name
```

## List files in a folder in bucket
```bash
aws s3 ls s3://bucket-name/public   
```

## Delete a bucket
```bash
aws s3 rb s3://bucket-name
aws s3 rb s3://bucket-name --force
```

## Sync local and s3 bucket
```bash
# Sync a folder
aws s3 sync <source> <target>

# sync a folder with file being public
aws s3 sync . s3://my-bucket/path --acl public-read
```

## Make files public in a bucket
```bash
aws s3 sync . s3://my-bucket/path --acl public-read
```

## Create a dynamodb table
```bash
aws dynamodb create-table \
    --table-name quotes \
    --attribute-definitions AttributeName=id,AttributeType=S \
    --key-schema AttributeName=id,KeyType=HASH \
    --provisioned-throughput ReadCapacityUnits=1,WriteCapacityUnits=1
# Table Name - quote
# Columns Name - id: String
# Key id:hash (Like primary key)
# Last line has something to do with billing, just copy paste for now
```



