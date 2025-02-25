# AWS Services Overview

This document provides an overview of key AWS services commonly used in data processing and cloud infrastructure management.

## Table of Contents
- [Amazon S3](#amazon-s3)
- [AWS IAM](#aws-iam)
- [Apache Spark Ecosystem](#apache-spark-ecosystem) (for comparison)
- [Databricks](#databricks) (for comparison)

## Amazon S3

Simple Storage Service (S3) is AWS's object storage service that offers industry-leading scalability, data availability, security, and performance.

### Core Concepts

#### Buckets
- Root-level containers for objects
- Globally unique names required
- Region-specific deployment

```python
# Creating an S3 bucket with boto3
import boto3
s3 = boto3.client('s3')
s3.create_bucket(Bucket='my-unique-bucket-name')
```

#### Objects
- Files and their metadata stored in buckets
- Up to 5TB per object
- Identified by unique keys
- Support for versioning

```python
# Uploading a file to S3
s3.upload_file('local_file.txt', 'my-bucket', 'folder/file.txt')

# Downloading a file from S3
s3.download_file('my-bucket', 'folder/file.txt', 'downloaded_file.txt')
```

### Storage Classes

| Storage Class | Use Case | Retrieval Time | Cost |
|---------------|----------|----------------|------|
| Standard | Frequently accessed data | Immediate | Higher |
| Standard-IA | Infrequent access | Immediate | Medium |
| One Zone-IA | Non-critical, infrequent access | Immediate | Lower |
| Glacier | Long-term archival | Hours | Very low |
| Glacier Deep Archive | Rarely accessed archival | Days | Lowest |

### Key Features

- **Security**: Bucket policies, ACLs, encryption (SSE, CSE)
- **Lifecycle Management**: Automatic transition between storage classes
- **Transfer Acceleration**: Faster uploads over long distances
- **Versioning**: Keep multiple versions of objects
- **Event Notifications**: Trigger workflows when objects change
- **Static Website Hosting**: Host websites directly from S3

## AWS IAM

Identity and Access Management (IAM) enables you to manage access to AWS services and resources securely.

### Core Components

#### Users
Individual identities for people or services with unique credentials.

```bash
# Creating a user
aws iam create-user --user-name johndoe
```

#### Groups
Collections of users that simplify permission management.

```bash
# Creating a group and adding users
aws iam create-group --group-name Developers
aws iam add-user-to-group --user-name johndoe --group-name Developers
```

#### Roles
Temporary identities that can be assumed by entities, used for delegation.

```json
// Example role trust policy
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": { "Service": "ec2.amazonaws.com" },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

#### Policies
JSON documents that define permissions.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::my-bucket",
        "arn:aws:s3:::my-bucket/*"
      ]
    }
  ]
}
```

### Best Practices

1. Follow the principle of least privilege
2. Use MFA for all privileged users
3. Rotate credentials regularly
4. Use roles for applications and services
5. Regularly audit permissions using IAM Access Analyzer

## Apache Spark Ecosystem

For comparison with AWS data processing services.

### Core Components

- **Spark Core**: Foundation with RDD APIs and task scheduling
- **Spark SQL**: Structured data processing with DataFrames and SQL
- **Spark Streaming**: Near real-time data processing
- **MLlib**: Machine learning library
- **GraphX**: Graph computation engine

### Language APIs

- Scala (native)
- Java
- Python (PySpark)
- R (SparkR)

## Databricks

Cloud-based platform built on top of Apache Spark.

### Key Features

- Managed Spark clusters
- Collaborative notebooks
- Delta Lake (ACID transactions)
- MLflow integration
- Unity Catalog
- Workflow orchestration

### AWS Alternatives

- Amazon EMR (Elastic MapReduce)
- AWS Glue
- Amazon Athena (for SQL queries)

---

## Contributing

Please submit a pull request for any updates or additional AWS services information.

## License

This document is licensed under the MIT License.
