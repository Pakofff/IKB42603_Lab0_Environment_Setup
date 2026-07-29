# IKB42603 — Lab 0: Environment Setup

> A verified local cloud-computing environment using Docker, LocalStack, Kubernetes, and AWS CLI.

## Overview

This repository documents the Lab 0 environment setup and verification. The setup provides a local AWS-compatible environment with **LocalStack**, together with a local Kubernetes cluster created using **kind**.

| Component | Purpose | Verification |
| :-- | :-- | :-- |
| Docker | Runs containerised services | `docker --version` |
| AWS CLI v2 | Interacts with AWS-compatible services | `aws --version` |
| LocalStack | Local AWS cloud-service emulator | Health endpoint |
| kind | Creates a local Kubernetes cluster | `kind --version` |
| kubectl | Manages the Kubernetes cluster | `kubectl version --client` |
| OpenSSL | Cryptographic utility | `openssl version` |
| oathtool | One-time-password utility | `oathtool --version` |

## Quick start

### 1. Check the required tools

```bash
docker --version
aws --version
kind --version
kubectl version --client
openssl version
oathtool --version
```

### 2. Start LocalStack and confirm its health

```bash
docker start localstack
curl http://localhost:4566/_localstack/health
```

### 3. Create the Kubernetes cluster

```bash
kind create cluster --name ccse
kubectl cluster-info --context kind-ccse
kubectl get nodes
```

### 4. Configure AWS CLI for LocalStack

```bash
aws configure set aws_access_key_id test
aws configure set aws_secret_access_key test
aws configure set region us-east-1
$EP='--endpoint-url=http://localhost:4566'
aws $EP sts get-caller-identity
```

## Verification evidence

<table>
  <tr>
    <td width="50%"><strong>Docker installed</strong><br><img src="Docker%20%281%29.png" alt="Docker version check"></td>
    <td width="50%"><strong>AWS CLI v2 installed</strong><br><img src="AWS%20CLI%20V2%20%282%29.png" alt="AWS CLI version check"></td>
  </tr>
  <tr>
    <td><strong>kind installed</strong><br><img src="Kind%20%283%29.png" alt="kind version check"></td>
    <td><strong>kubectl installed</strong><br><img src="Kubectl%20%284%29.png" alt="kubectl client version check"></td>
  </tr>
  <tr>
    <td><strong>OpenSSL installed</strong><br><img src="OpenSSL%20%285%29.png" alt="OpenSSL version check"></td>
    <td><strong>oathtool installed</strong><br><img src="Oathtool%20%286%29.png" alt="oathtool version check"></td>
  </tr>
</table>

### LocalStack health check

The LocalStack health endpoint confirms that local cloud services are available.

![LocalStack health response](Docker%20run%20%287%29.png)

### Kubernetes cluster verification

The `ccse` cluster was created successfully and its control-plane node is ready.

![kind cluster creation and node verification](Create%20Cluster.png)

### AWS CLI LocalStack configuration

The AWS CLI is configured with test credentials and uses the LocalStack endpoint at `http://localhost:4566`.

![AWS CLI LocalStack configuration](AWS%20CLI%20Configuration.png)

## Detailed guide

For the complete step-by-step procedure and all screenshots, see [the environment setup cheatsheet](IKB42603_Lab0_Environment_Setup_Cheatsheet.md).

## Expected outcome

- All required CLI tools are installed and accessible.
- LocalStack services are available locally on port `4566`.
- The `kind-ccse` Kubernetes context is active and its node is ready.
- AWS CLI requests can be sent to LocalStack successfully.
