# Module 03: Build and Run a Bootable LAMP Disk Image

## Brief Overview

This module demonstrates the core capability of image mode for RHEL: converting the LAMP application container built in Module 2 into a bootable virtual machine disk image. Learners will use Podman Desktop's bootable container extensions to build a qcow2 disk image from their containerized LAMP application, then launch it as a running virtual machine. This hands-on workflow shows how container images can be transformed into immutable, bootable operating system images suitable for cloud deployment or bare metal installation.

## Audience and Time

**Target personas:** Developers, platform engineers, DevOps engineers (beginner level)

**Prerequisites for this module:**
- Completed Module 1 (authenticated to Red Hat Container Registry)
- Completed Module 2 (built and tested LAMP development container)
- Understanding of virtual machine concepts
- Familiarity with systemd service configuration

**Estimated duration:** 30 minutes

## Learning Objectives

- Build bootable container images from Containerfiles using image mode for RHEL
- Convert container images to virtual machine disk images in qcow2 format
- Deploy and launch bootable container images as running virtual machines
- Configure systemd services to start automatically in bootable container environments
- Verify that containerized applications run successfully in booted VM instances

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Prepare the bootable Containerfile | 8 min |
| 2 | Build the bootable container image | 7 min |
| 3 | Generate the qcow2 disk image | 8 min |
| 4 | Launch and verify the bootable VM | 7 min |

## Detailed Steps

1. Navigate to your `lamp-app` project directory from Module 2
2. Create a new file named `Containerfile.bootable` in the project directory
3. Copy the content from your existing `Containerfile` as the starting point
4. Update the FROM instruction to use the RHEL bootc base image: `FROM registry.redhat.io/rhel10-beta/rhel-bootc:latest`
5. Keep the existing RUN instruction to install httpd, mariadb-server, php, and php-mysqlnd
6. Update the systemctl enable instruction to ensure services start on boot: `RUN systemctl enable httpd mariadb`
7. Add RUN instruction to create the MariaDB data directory: `RUN mysql_install_db --user=mysql --datadir=/var/lib/mysql`
8. Keep the COPY instructions for `scripts/init-db.sql` and `index.php`
9. Add a RUN instruction to create a systemd service unit for database initialization
10. Create the service unit content to run `mysql -u root < /tmp/init-db.sql` on first boot
11. Add RUN instruction to enable the database initialization service
12. Remove the CMD instruction (bootc images use systemd as init automatically)
13. Save the `Containerfile.bootable` file
14. Open Podman Desktop and navigate to the Bootable Containers section
15. Click "Build bootable image"
16. Select the `lamp-app` directory and choose `Containerfile.bootable` as the build file
17. Set the image name to `lamp-bootable:latest`
18. Click Build and observe the bootc build process in the console output
19. Verify that the build completes successfully and shows no errors
20. Confirm the `lamp-bootable:latest` image appears in the Bootable Containers → Images list
21. Navigate to Bootable Containers → Disk Images in Podman Desktop
22. Click "Create disk image"
23. Select the `lamp-bootable:latest` image as the source
24. Choose qcow2 as the output format
25. Set the disk image name to `lamp-bootable-disk.qcow2`
26. Configure disk size to 20 GB (sufficient for RHEL and LAMP stack)
27. Click "Build disk image"
28. Observe the image conversion process (may take several minutes)
29. Monitor the progress indicator showing the qcow2 generation
30. Verify successful completion when the disk image appears in the Disk Images list
31. Navigate to Bootable Containers → Virtual Machines in Podman Desktop
32. Click "Launch VM from disk image"
33. Select the `lamp-bootable-disk.qcow2` image
34. Set the VM name to `lamp-vm`
35. Allocate 2 GB RAM and 2 vCPUs for the VM
36. Enable port forwarding to map VM port 80 to host port 9090
37. Click "Start VM"
38. Observe the boot process in the VM console view
39. Wait for the systemd boot sequence to complete (showing login prompt)
40. Verify that the systemd services started successfully (check console output for httpd and mariadb)
41. Open a web browser on your local workstation
42. Navigate to `http://127.0.0.1:9090`
43. Verify that the page displays "Hello, World!" from the database running inside the booted VM
44. Alternatively, open a terminal and run `curl http://127.0.0.1:9090`
45. Confirm the HTML response matches the output from Module 2
46. Return to Podman Desktop and observe the VM status showing "Running"
47. Review the Disk Images dashboard confirming the bootable image build and deployment

## Key Takeaways

- Image mode for RHEL enables building bootable operating system images using standard Containerfile syntax
- The rhel-bootc base image provides the foundation for bootable container images with systemd integration
- Container images can be converted to industry-standard disk image formats (qcow2) for VM deployment
- Services configured with systemctl in the Containerfile start automatically when the bootable image boots
- The same application that ran in a development container (Module 2) runs identically in a booted VM instance
- Bootable container images are immutable — updates are deployed by building and booting new image versions
- The container-to-disk workflow unifies application packaging across development, testing, and production environments
- Port forwarding enables local access to services running inside booted VM instances

## Infrastructure Notes

No server-side infrastructure required. All operations are performed locally on the student's workstation using Podman Desktop with the bootable containers extension. The VM runs using the local hypervisor (QEMU/KVM on Linux, HVF on macOS, Hyper-V on Windows). Port 9090 is used on the host to differentiate from the development container in Module 2 (which used port 8080).
