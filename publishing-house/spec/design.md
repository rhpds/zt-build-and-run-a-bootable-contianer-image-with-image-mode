# Build and Run a Bootable Container Image with Image Mode for RHEL and Podman Desktop

## Overview

Image mode for Red Hat Enterprise Linux uses a container-native approach to build, deploy, and manage the operating system as a bootable container. This enables developers to bundle runtimes, drivers, dependencies, and applications into a single bootable container image that can be converted to bootable cloud images or bare metal installers.

Participants will authenticate to the Red Hat Container Registry using Podman Desktop, build a LAMP (Linux, Apache, MariaDB, PHP) application within a development container environment, and package the application as an immutable bootable container image that can be deployed as a virtual machine disk image.

## Target Audience

- **Role:** Developers, platform engineers, DevOps engineers
- **Experience level:** Beginner
- **What they already know:** Basic Linux file system navigation, creating and editing text files, understanding of LAMP stack components (PHP, MariaDB, Apache webserver)
- **What they don't know:** Image mode for RHEL, bootable containers, container-to-disk conversion workflows, systemd service configuration in containerized environments

## Prerequisites

- No-cost Red Hat Developer subscription (register at developers.redhat.com)
- Podman Desktop installed on Windows, macOS, or Linux
- Basic understanding of Linux command line
- Basic understanding of text file editing
- Basic familiarity with PHP, MariaDB, and Apache webserver concepts
- **Validation:** No — prerequisites are verified through Red Hat SSO login and Podman Desktop installation check at lab start

## Learning Objectives

1. Configure Red Hat SSO authentication in Podman Desktop to access the Red Hat Container Registry
2. Build a LAMP application development environment using RHEL Universal Base Image containers
3. Create and configure MariaDB databases with automated initialization scripts
4. Build bootable container images from Containerfiles using image mode for RHEL
5. Deploy bootable container images as virtual machine disk images in qcow2 format

## Content Type

Lab (hands-on)

## Products & Technologies

- Red Hat Enterprise Linux 10
- Podman Desktop
- Image mode for Red Hat Enterprise Linux
- Red Hat Universal Base Image (UBI) 10
- Apache HTTP Server
- MariaDB
- PHP

## Module Map

| Module | Title | Duration |
|--------|-------|----------|
| 1 | Access the Red Hat Container Registry | 10 min |
| 2 | Build a LAMP development container | 25 min |
| 3 | Build and run a bootable LAMP disk image | 30 min |
| — | **Total hands-on** | **65 min** |
| — | Intro / presentation | ~10 min |
| — | **Total lab** | **~75 min** |

## Difficulty Level

Beginner

## Environment

**Learner view:** Students start with Podman Desktop pre-installed on their local workstation (Windows, macOS, or Linux). The Red Hat extensions for bootable containers, subscription, registry, and VM management are pre-installed in Podman Desktop. Students will work entirely in their local desktop environment — no cloud infrastructure or remote clusters are required. The lab runs completely on the student's local machine.

**Automation needed:** No

No server-side automation is required. All work is performed locally in Podman Desktop on the student's desktop or laptop. Students manually build containers, configure services, and generate disk images through the Podman Desktop UI and container terminal.

## Infrastructure Requirements

- **Cloud provider:** CNV (supports nested virtualization)
- **Platform:** RHEL VMs (1 per student)
- **Per student:** 1 RHEL 10 build host (8 vCPU, 32GB RAM, 150GB disk) with Podman Desktop pre-installed
  - **Note:** This host runs nested virtualization — students build bootable container images and deploy them as nested KVM guests within Podman Desktop
- **Topology:** Per-student
- **Automation approach:** Ansible (pre-install Podman Desktop, configure Red Hat extensions for bootc/registry/VM)
- **AI/MaaS:** None
- **External services:** registry.redhat.io (Red Hat Container Registry for pulling UBI and bootc base images)
- **AAP version:** N/A — Ansible Automation Platform not used in this lab
- **Non-GA products:** None (all products are GA)

## Assessment Strategy

This is a zero-touch guided lab with solve/validate verification at key checkpoints:

- **Module 1:** Validate Red Hat SSO authentication status shows "LOGGED IN" in Podman Desktop Settings → Authentication
- **Module 2:** Validate LAMP development container is running and `curl 127.0.0.1` returns "Hello, World!" HTML response
- **Module 3:** Validate bootable disk image build completes successfully and appears in "Bootable Containers > Disk Images" dashboard; validate VM launches with the built disk image

## Design Principles

**Execution-first, minimal exposition.** Each module prioritizes hands-on action over reading. Learners should spend 70% of their time executing commands, clicking UI elements, and seeing immediate results — not reading concept explanations.

- **Front-load the payoff:** Show what they'll build in the first paragraph with a screenshot
- **Minimize concept blocks:** Just enough context to understand WHY, then jump to HOW
- **Immediate verification:** After every 3-5 steps, include a "Check: you should see X" checkpoint
- **Visual progress:** Use screenshots at key moments to confirm they're on track
- **Incremental wins:** Every module ends with a visible, testable result (logged in status, working web app, booted VM)
