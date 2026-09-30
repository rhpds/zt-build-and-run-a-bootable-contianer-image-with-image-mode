# Module 01: Access the Red Hat Container Registry

## Brief Overview

This module introduces participants to Red Hat SSO authentication in Podman Desktop. Learners will configure their Podman Desktop installation to authenticate with the Red Hat Container Registry using their Red Hat Developer subscription credentials. By the end of this module, participants will have verified access to pull RHEL Universal Base Images and other Red Hat container images required for subsequent modules.

## Audience and Time

**Target personas:** Developers, platform engineers, DevOps engineers (beginner level)

**Prerequisites for this module:**
- Valid Red Hat Developer subscription (free at developers.redhat.com)
- Podman Desktop installed on Windows, macOS, or Linux
- Red Hat extensions for bootable containers, subscription, registry, and VM management pre-installed in Podman Desktop

**Estimated duration:** 10 minutes

## Learning Objectives

- Configure Red Hat SSO authentication in Podman Desktop to access the Red Hat Container Registry
- Verify successful authentication status through Podman Desktop UI
- Confirm ability to pull Red Hat Universal Base Image containers from the authenticated registry

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Launch Podman Desktop and locate authentication settings | 2 min |
| 2 | Authenticate with Red Hat SSO | 5 min |
| 3 | Verify registry access | 3 min |

## Detailed Steps

1. Launch Podman Desktop application on your local workstation
2. Navigate to Settings → Authentication from the left sidebar menu
3. Locate the Red Hat Container Registry authentication section
4. Click "Login with Red Hat SSO"
5. Complete authentication in the browser window that opens (Red Hat SSO login flow)
6. Enter Red Hat Developer subscription credentials (username and password)
7. Authorize Podman Desktop to access your Red Hat account
8. Return to Podman Desktop and observe authentication status
9. Verify that authentication status shows "LOGGED IN" in Settings → Authentication
10. Navigate to Images section in Podman Desktop
11. Click "Pull an image" button
12. Enter `registry.redhat.io/ubi10/ubi:latest` in the image name field
13. Click Pull to download the Red Hat Universal Base Image
14. Observe successful pull operation in the Images list
15. Verify that the UBI 10 image appears in your local image registry

## Key Takeaways

- Red Hat SSO provides centralized authentication for Red Hat services including the container registry
- Podman Desktop integrates Red Hat authentication directly into the UI workflow
- The Red Hat Container Registry (registry.redhat.io) hosts official Red Hat product container images
- Red Hat Universal Base Image (UBI) is freely redistributable and serves as the foundation for building bootable containers
- Successful authentication enables access to the full catalog of Red Hat container images required for image mode workflows

## Infrastructure Notes

No server-side infrastructure required. All operations are performed locally on the student's workstation. Network connectivity to registry.redhat.io and sso.redhat.com is required for authentication and image pulls.
