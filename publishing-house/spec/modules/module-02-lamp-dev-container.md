# Module 02: Build a LAMP Development Container

## Brief Overview

This module guides participants through building a complete LAMP (Linux, Apache, MariaDB, PHP) application development environment using RHEL Universal Base Image containers. Learners will create a Containerfile that installs and configures Apache HTTP Server, MariaDB database server, and PHP runtime, then build and run the containerized application locally. The module emphasizes hands-on container building, database initialization scripting, and service configuration within a development container environment.

## Audience and Time

**Target personas:** Developers, platform engineers, DevOps engineers (beginner level)

**Prerequisites for this module:**
- Completed Module 1 (authenticated to Red Hat Container Registry)
- Basic understanding of LAMP stack components (PHP, MariaDB, Apache webserver)
- Basic Linux command line familiarity
- Text file editing skills

**Estimated duration:** 25 minutes

## Learning Objectives

- Build a LAMP application development environment using RHEL Universal Base Image containers
- Create and configure MariaDB databases with automated initialization scripts
- Configure Apache HTTP Server to serve PHP applications within a container
- Verify running web applications with local HTTP requests
- Understand the container development workflow for building LAMP stack applications

## Lab Structure

| Section | Title | Duration |
|---------|-------|----------|
| 1 | Create the LAMP Containerfile | 8 min |
| 2 | Add MariaDB database initialization script | 5 min |
| 3 | Build and run the LAMP development container | 7 min |
| 4 | Test the running LAMP application | 5 min |

## Detailed Steps

1. Create a new project directory named `lamp-app` on your local workstation
2. Navigate into the `lamp-app` directory
3. Create a new file named `Containerfile` in the project directory
4. Add `FROM registry.redhat.io/ubi10/ubi:latest` as the base image instruction
5. Add `RUN dnf install -y httpd mariadb-server php php-mysqlnd` to install LAMP stack components
6. Add `RUN systemctl enable httpd mariadb` to configure services to start automatically
7. Add `EXPOSE 80` to expose the Apache HTTP port
8. Add `CMD ["/sbin/init"]` to set systemd as the container entry point
9. Save the Containerfile
10. Create a subdirectory named `scripts` in the project directory
11. Create a file named `init-db.sql` inside the `scripts` directory
12. Add SQL commands to create a sample database named `appdb`
13. Add SQL commands to create a database user with appropriate permissions
14. Add SQL commands to create a simple `messages` table with `id` and `content` columns
15. Add SQL command to insert a test record: "Hello, World!"
16. Save the `init-db.sql` file
17. Update the Containerfile to copy `scripts/init-db.sql` to `/tmp/init-db.sql` in the container
18. Add a RUN instruction to initialize the MariaDB data directory
19. Create a file named `index.php` in the project directory
20. Add PHP code to connect to MariaDB using localhost connection
21. Add PHP code to query the `messages` table and retrieve the test record
22. Add PHP code to output the message content as HTML
23. Save the `index.php` file
24. Update the Containerfile to copy `index.php` to `/var/www/html/index.php` in the container
25. Open Podman Desktop and navigate to Images section
26. Click "Build an image" button
27. Select the `lamp-app` directory containing your Containerfile
28. Set the image name to `lamp-dev:latest`
29. Click Build and observe the build process in the console output
30. Verify successful build completion in the Images list
31. Navigate to Containers section in Podman Desktop
32. Click "Create container" from the `lamp-dev:latest` image
33. Set container name to `lamp-dev-container`
34. Map port 80 from the container to port 8080 on the host
35. Enable privileged mode to allow systemd to run properly
36. Click "Start container"
37. Observe container status showing "Running" in the Containers list
38. Open the container terminal in Podman Desktop
39. Run `mysql -u root < /tmp/init-db.sql` to initialize the database
40. Verify database initialization completed successfully
41. Run `systemctl restart httpd` to ensure Apache is serving the PHP application
42. Open a web browser on your local workstation
43. Navigate to `http://127.0.0.1:8080`
44. Verify that the page displays "Hello, World!" from the database query
45. Alternatively, open a terminal and run `curl http://127.0.0.1:8080`
46. Confirm the HTML response contains "Hello, World!"

## Key Takeaways

- Red Hat Universal Base Image provides a complete RHEL foundation for building containerized applications
- Containerfiles define reproducible build steps for installing and configuring application stacks
- MariaDB database initialization can be automated using SQL scripts executed at container startup
- Apache HTTP Server and PHP work together in containers just as they do on traditional RHEL installations
- Systemd can run as the container init process to manage multiple services within a single container
- Port mapping enables local access to containerized web applications during development
- The development container workflow provides immediate feedback through local testing before building bootable images

## Infrastructure Notes

No server-side infrastructure required. All operations are performed locally on the student's workstation using Podman Desktop. The container runs with privileged mode enabled to allow systemd to manage services. Port 8080 is used on the host to avoid conflicts with existing HTTP services.
