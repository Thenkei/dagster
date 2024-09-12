---
layout: Integration
status: published
name: AWS S3
title: Dagster & AWS S3
sidebar_label: AWS S3
excerpt: The AWS S3 integration allows data engineers to easily read and write objects to the durable AWS S3 storage, enabling engineers to have a resilient storage layer when constructing their pipelines.
date: 2024-06-21
apireflink: https://docs.dagster.io/_apidocs/libraries/dagster-aws
docslink: 
partnerlink: https://aws.amazon.com/
logo: /integrations/aws-s3.svg
categories:
  - Storage
enabledBy:
enables:
---

### About this integration

The AWS S3 integration allows data engineers to easily read, and write objects to the durable AWS S3 storage -- enabling engineers to a resilient storage layer when constructing their pipelines.

### Installation

```bash
pip install dagster-aws
```

### Examples

Here is an example of how to use the `S3Resource` in a Dagster job to interact with AWS S3:

```python

import pandas as pd
from dagster import Definitions, asset
from dagster_aws.s3 import S3Resource


@asset
def my_s3_asset(s3: S3Resource):
    df = pd.DataFrame({"column1": [1, 2, 3], "column2": ["A", "B", "C"]})

    csv_data = df.to_csv(index=False)

    s3_client = s3.get_client()

    s3_client.put_object(
        Bucket="my-cool-bucket",
        Key="path/to/my_dataframe.csv",
        Body=csv_data,
    )


defs = Definitions(
    assets=[my_s3_asset],
    resources={"s3": S3Resource(region_name="us-west-2")},
)
```

```

### About AWS S3

**Amazon Simple Storage Service (Amazon S3)** is an object storage service that offers industry-leading scalability, data availability, security, and performance. This means customers of all sizes and industries can use it to store and protect any amount of data for a range of use cases, such as data lakes, websites, mobile applications, backup and restore, archive, enterprise applications, IoT devices, and big data analytics. Amazon S3 provides easy-to-use management features so you can organize your data and configure finely-tuned access controls to meet your specific business, organizational, and compliance requirements.
```