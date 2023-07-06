# SSH Bastion Server Helm Chart

This Helm chart deploys a Kubernetes Bastion SSH Server. It sets up a deployment, service, persistent volume claim, and configures SSH access with authorized keys.

The logs of the SSH accesses into the bastion are stored in the configured PV.

## Prerequisites

- Kubernetes cluster
- Helm 3 or later

## Installation

1. Add the Helm chart repository:

```bash
   helm repo add ssh-bastion <repository-url>
   helm repo update
```

2. Install the SSH Bastion Server chart:

```bash
   helm install my-ssh-bastion ssh-bastion/ssh-bastion
```

## Configuration

The following table lists some configurable parameters and their default values for the SSH Bastion Server chart.

| Parameter                 | Description                          | Default        |
|---------------------------|--------------------------------------|----------------|
| `replicaCount`            | Number of replicas for the deployment | `1`            |
| `sshConfig.authorizedKeys`| SSH authorized keys                   | `` |
| `service.type`            | Service type                          | `LoadBalancer`    |
| `service.port`            | Service port                          | `22`           |
| `logs.enabled`   | Store SSH connection logs                | `true`      |
| `logs.storageClassName`   | Storage class for logs                | `csi-cinder-default`      |
| `logs.size`   | Storage size for logs                | `10Gi`      |

Specify each parameter using the `--set key=value[,key=value]` argument during installation. Alternatively, you can create a YAML file containing the values and provide it to the installation command using the `-f` or `--values` flag.

## SSH Authorized Keys

You can specify the SSH authorized keys by modifying the `values.yaml` file. Add or remove entries in the `sshConfig.authorizedKeys` section, following the given format:

sshConfig:
  authorizedKeys:
    username1: ssh-rsa <public-key>
    username2: ssh-rsa <public-key>
    ...

## Accessing the SSH Bastion Server

Once the SSH Bastion Server is deployed, you can access it using SSH. Use the following command:

```bash
ssh -i <private-key> <username>@<ssh-bastion-service-ip>
```

Replace `<private-key>` with the path to your private key file, `<username>` with the desired username, and `<ssh-bastion-service-ip>` with the IP address of the SSH Bastion service.

## Uninstallation

To uninstall the SSH Bastion Server chart, run the following command:

```bash
helm uninstall my-ssh-bastion
```

This will remove all resources associated with the chart from your Kubernetes cluster.

For more information on chart configuration and customization options, refer to the chart documentation.

## License

MIT License

