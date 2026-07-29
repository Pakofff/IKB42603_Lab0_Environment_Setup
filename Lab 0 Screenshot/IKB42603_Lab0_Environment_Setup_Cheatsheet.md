# IKB42603 Lab 0 — Environment Setup Cheatsheet
Name: Muhammad Aqeef Firhat Bin Mohd Rodzi

Student ID: 52215125820

Class: L02-B04

This guide records the completed Lab 0 environment setup. Each section includes the corresponding terminal screenshot as evidence of the completed step.

## 1. Verify Docker

Confirm that Docker is installed and available from the terminal:

```bash
docker --version
```

![Docker version check](Docker%20%281%29.png)

## 2. Verify AWS CLI v2

Confirm that the AWS CLI is installed:

```bash
aws --version
```

![AWS CLI version check](AWS%20CLI%20V2%20%282%29.png)

## 3. Verify kind

Confirm that kind (Kubernetes IN Docker) is installed:

```bash
kind --version
```

![kind version check](Kind%20%283%29.png)

## 4. Verify kubectl

Confirm that the Kubernetes command-line client is installed:

```bash
kubectl version --client
```

![kubectl client version check](Kubectl%20%284%29.png)

## 5. Verify OpenSSL

Confirm that OpenSSL is installed:

```bash
openssl version
```

![OpenSSL version check](OpenSSL%20%285%29.png)

## 6. Verify oathtool

Confirm that the OATH Toolkit utility is installed:

```bash
oathtool --version
```

![oathtool version check](Oathtool%20%286%29.png)

## 7. Check LocalStack

With the LocalStack Docker container running, query its health endpoint:

```bash
curl http://localhost:4566/_localstack/health
```

The response should list the available LocalStack services.

![LocalStack health response](Docker%20run%20%287%29.png)

## 8. Create and verify the kind cluster

Create the Kubernetes cluster named `ccse`:

```bash
kind create cluster --name ccse
```

Verify that the control plane is reachable and the node is ready:

```bash
kubectl cluster-info --context kind-ccse
kubectl get nodes
```

![kind cluster creation and node verification](Create%20Cluster.png)

## 9. Configure AWS CLI for LocalStack

Set test credentials and the AWS region:

```bash
aws configure set aws_access_key_id test
aws configure set aws_secret_access_key test
aws configure set region us-east-1
```

Set the LocalStack endpoint for the current shell, then verify the configuration:

```bash
$EP='--endpoint-url=http://localhost:4566'
aws $EP sts get-caller-identity
```

Start the container again when it is stopped:

```bash
docker start localstack
```

![AWS CLI LocalStack configuration](AWS%20CLI%20Configuration.png)

## Completion checklist

- Docker, AWS CLI, kind, kubectl, OpenSSL, and oathtool are installed.
- LocalStack reports its services as available.
- The `ccse` kind cluster is running and its control-plane node is ready.
- AWS CLI can call LocalStack using the local endpoint.
