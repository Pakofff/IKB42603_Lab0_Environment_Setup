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

## Detailed guide

For the complete step-by-step procedure and all screenshots, see [the environment setup cheatsheet](IKB42603_Lab0_Environment_Setup_Cheatsheet.md).

## Expected outcome

- All required CLI tools are installed and accessible.
- LocalStack services are available locally on port `4566`.
- The `kind-ccse` Kubernetes context is active and its node is ready.
- AWS CLI requests can be sent to LocalStack successfully.
