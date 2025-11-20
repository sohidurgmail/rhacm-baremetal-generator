# RHACM Baremetal Cluster YAML Generator

This repo generates all required YAML manifests to create a **baremetal managed cluster** on an RHACM/MCE hub, from a CSV of nodes and a small set of cluster variables.

## What it does

`ansible-playbook generate-mce-yamls.yml` reads:

- `nodes.csv` – one row per node (Worker nodes, Red Hat Core OS, iLO IP, MACs, etc.).
- `vars/cluster.yml` – cluster-level settings (name, base domain, VIPs, etc.).
- `templates/*.j2` – Jinja2 templates for RHACM/MCE objects.

and produces in `out/`:

- `cluster-namespace.yaml`
- `cluster-deployment.yaml`
- `cluster-agentclusterinstall.yaml`
- `managedcluster.yaml`g
- `klusterletaddonconfig.yaml`
- `cluster-infraenv-ns.yaml`
- `cluster-infraenv.yaml`
- `pullsecret-cluster-secret.yaml`
- `baremetalhost-<node>.yaml` (one per node)
- `bmc-secret.yaml` (BMC secrets for all nodes)

These can then be applied to the hub cluster to create and manage the baremetal OpenShift cluster.

## Prerequisites

- Ansible
- `community.general` collection:

```bash
ansible-galaxy collection install community.general
