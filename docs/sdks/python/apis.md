---
title: API Wrapper
id: apis
sidebar_label: APIs
description: "Learn how to manage computational resources with the RunPod API, including endpoint configurations, template creation, and GPU management, to optimize your project's performance."
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

This document outlines the core functionalities provided by the RunPod API, including how to interact with Endpoints, manage Templates, and list available GPUs.
These operations let you dynamically manage computational resources within the RunPod environment.

## Get Endpoints

To retrieve a comprehensive list of all available endpoint configurations within RunPod, you can use the `get_endpoints()` function.
This function returns a list of endpoint configurations, allowing you to understand what's available for use in your projects.

```python
import runpod
import os

runpod.api_key = os.getenv("RUNPOD_API_KEY")

# Fetching all available endpoints
endpoints = runpod.get_endpoints()

# Displaying the list of endpoints
print(endpoints)
```

## Create Template

Templates in RunPod serve as predefined configurations for setting up environments efficiently.
The `create_template()` function facilitates the creation of new templates by specifying a name and a Docker image.

<Tabs>
  <TabItem value="python" label="Python" default>

```python
import runpod
import os

runpod.api_key = os.getenv("RUNPOD_API_KEY")

try:
    # Creating a new template with a specified name and Docker image
    new_template = runpod.create_template(name="test", image_name="runpod/base:0.1.0")

    # Output the created template details
    print(new_template)

except runpod.error.QueryError as err:
    # Handling potential errors during template creation
    print(err)
    print(err.query)
```

</TabItem>
  <TabItem value="output" label="Output">

```json
{
  "id": "n6m0htekvq",
  "name": "test",
  "imageName": "runpod/base:0.1.0",
  "dockerArgs": "",
  "containerDiskInGb": 10,
  "volumeInGb": 0,
  "volumeMountPath": "/workspace",
  "ports": "",
  "env": [],
  "isServerless": false
}
```

</TabItem>
</Tabs>

## Create Endpoint

Creating a new endpoint with the `create_endpoint()` function.
This function requires you to specify a `name` and a `template_id`.
Additional configurations such as GPUs, number of Workers, and more can also be specified depending your requirements.

<Tabs>
  <TabItem value="python" label="Python" default>

```python
import runpod
import os

runpod.api_key = os.getenv("RUNPOD_API_KEY")

try:
    # Creating a template to use with the new endpoint
    new_template = runpod.create_template(
        name="test", image_name="runpod/base:0.4.4", is_serverless=True
    )

    # Output the created template details
    print(new_template)

    # Creating a new endpoint using the previously created template
    new_endpoint = runpod.create_endpoint(
        name="test",
        template_id=new_template["id"],
        gpu_ids="AMPERE_16",
        workers_min=0,
        workers_max=1,
    )

    # Output the created endpoint details
    print(new_endpoint)

except runpod.error.QueryError as err:
    # Handling potential errors during endpoint creation
    print(err)
    print(err.query)
```

</TabItem>
  <TabItem value="output" label="Output">

```json
{
  "id": "Unique_Id",
  "name": "YourTemplate",
  "imageName": "runpod/base:0.4.4",
  "dockerArgs": "",
  "containerDiskInGb": 10,
  "volumeInGb": 0,
  "volumeMountPath": "/workspace",
  "ports": null,
  "env": [],
  "isServerless": true
}
{
  "id": "Unique_Id",
  "name": "YourTemplate",
  "templateId": "Unique_Id",
  "gpuIds": "AMPERE_16",
  "networkVolumeId": null,
  "locations": null,
  "idleTimeout": 5,
  "scalerType": "QUEUE_DELAY",
  "scalerValue": 4,
  "workersMin": 0,
  "workersMax": 1
}
```

</TabItem>
</Tabs>

## Get GPUs

For understanding the computational resources available, the `get_gpus()` function lists all GPUs that can be allocated to endpoints in RunPod. This enables optimal resource selection based on your computational needs.

<Tabs>
  <TabItem value="python" label="Python" default>

```python
import runpod
import json
import os

runpod.api_key = os.getenv("RUNPOD_API_KEY")

# Fetching all available GPUs
gpus = runpod.get_gpus()

# Displaying the GPUs in a formatted manner
print(json.dumps(gpus, indent=2))
```

</TabItem>
  <TabItem value="output" label="Output">

```json
[
  {
    "id": "NVIDIA A100 80GB PCIe",
    "displayName": "A100 80GB",
    "memoryInGb": 80
  },
  {
    "id": "NVIDIA A100-SXM4-80GB",
    "displayName": "A100 SXM 80GB",
    "memoryInGb": 80
  }
  // Additional GPUs omitted for brevity
]
```

</TabItem>
</Tabs>

## Get GPU by Id

Use `get_gpu()` and pass in a GPU Id to retrieve details about a specific GPU model by its ID.
This is useful when understanding the capabilities and costs associated with various GPU models.

<Tabs>
  <TabItem value="python" label="Python" default>

```python
import runpod
import json
import os

runpod.api_key = os.getenv("RUNPOD_API_KEY")

gpus = runpod.get_gpu("NVIDIA A100 80GB PCIe")

print(json.dumps(gpus, indent=2))
```

</TabItem>
  <TabItem value="output" label="Output">

```json
{
  "maxGpuCount": 8,
  "id": "NVIDIA A100 80GB PCIe",
  "displayName": "A100 80GB",
  "manufacturer": "Nvidia",
  "memoryInGb": 80,
  "cudaCores": 0,
  "secureCloud": true,
  "communityCloud": true,
  "securePrice": 1.89,
  "communityPrice": 1.59,
  "oneMonthPrice": null,
  "threeMonthPrice": null,
  "oneWeekPrice": null,
  "communitySpotPrice": 0.89,
  "secureSpotPrice": null,
  "lowestPrice": {
    "minimumBidPrice": 0.89,
    "uninterruptablePrice": 1.59
  }
}
```

</TabItem>

</Tabs>

Through these functionalities, the RunPod API enables efficient and flexible management of computational resources, catering to a wide range of project requirements.
