# AWS Ansible DevOps Monitoring Lab

A hands-on DevOps project demonstrating AWS networking, Linux administration,
Ansible automation, Docker containerization, Nginx deployment, and infrastructure
monitoring with Prometheus and Grafana.

## Architecture

Mac Workstation
        |
        | SSH
        v
Control Server
10.0.1.10
Ansible / Git
        |
        +--------------------+
        |                    |
        v                    v
App Server              Monitoring Server
10.0.2.10               10.0.3.10
Docker                   Docker
Nginx :80                Prometheus :9090
Node Exporter :9100      Grafana :3000

## AWS Network

- Region: us-east-1
- VPC: 10.0.0.0/16
- Public subnet: 10.0.1.0/24
- Application subnet: 10.0.2.0/24
- Monitoring subnet: 10.0.3.0/24
- Internet Gateway for the public subnet
- NAT Gateway for private-server outbound connectivity
- Security groups restrict communication between tiers

## Technologies

- AWS
- Ubuntu Linux
- Ansible
- Docker
- Nginx
- Prometheus
- Node Exporter
- Grafana
- Git
- GitHub
- SSH

## Ansible Automation

The control server manages the private application and monitoring servers.

Test connectivity:

    ansible all -i inventory.ini -m ping

Run server configuration:

    ansible-playbook -i inventory.ini setup.yml

Deploy Nginx:

    ansible-playbook -i inventory.ini deploy-nginx.yml

## Application

Nginx runs as a Docker container on `app01`.

Application endpoint inside the VPC:

    http://10.0.2.10

## Monitoring

Node Exporter collects Linux system metrics from `app01`.

    app01:9100
        |
        v
    Prometheus:9090
        |
        v
    Grafana:3000

Metrics include:

- CPU utilization
- Memory usage
- Disk usage
- Network statistics
- System load
- Uptime

Grafana Node Exporter Full dashboard is used to visualize the metrics.

## Security

- Application and monitoring instances do not require public IP addresses.
- SSH access is routed through the control/bastion server.
- Security groups restrict communication between servers.
- Grafana is accessed through SSH port forwarding.
- SSH private keys and secrets are excluded from Git.

## Skills Demonstrated

This project demonstrates hands-on experience with:

- AWS VPC networking
- Public and private subnet architecture
- Routing and NAT
- Linux server administration
- SSH bastion architecture
- Configuration management with Ansible
- Docker container deployment
- Web-server deployment
- Infrastructure monitoring
- Prometheus metrics collection
- Grafana visualization
- Git-based infrastructure workflows
