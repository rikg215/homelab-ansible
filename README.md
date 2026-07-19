# Homelab Ansible Configuration Repo

## Purpose:

This is a repo dedicated to my ansible configuration management for my homelab. 30 hosts (LXCs, VMs, k8s nodes) on Proxmox, managed from a dedicated control node.

## Inventory Layout

Inventory split into groups based on type as top level then function at a lower level. LXCs, VMS, Others, hypervisor, and homelab - top level. Examples for function grouping are, media-aquisition, nas, security and so on.  

## Access model

Dedicated ansible user on every host via SSH key auth no password. Passwordless sudo via drop in file /etc/sudoers.d/20-ansible-user. Bootstrap: first run uses -K with admin creds, every subsequent run uses ssh key auth with no need for a password.

## How to run

ansible-playbook site.yml --limit <group>. List all available --limit targets: automation, individual groups like k8s_cluster or tools, or homelab for the full fleet. Use --check or --diff for dry runs. 

## Managed vs excluded

Common role handles: Packages, NTP, hostname assignment, admin user. Hardening handles: ssh, sysctl, firewall, and autoupdates. This repo will NOT manage app configs, docker containers, or k8s manifests.
