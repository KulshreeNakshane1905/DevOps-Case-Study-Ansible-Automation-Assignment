# DevOps Case Study: Ansible Automation for EduTrack

## 1. Project Overview

**EduTrack** is a student learning dashboard designed to help students organize study tasks, manage assignments, track deadlines, and monitor their learning progress.

This project demonstrates how DevOps principles and Ansible automation can be used to configure and deploy a web application consistently and reliably.

The application is built using HTML, CSS, and JavaScript. Ansible automates the creation of the deployment directory, copies the application files, and verifies that deployment was successful.

## 2. Objectives

- Understand the DevOps lifecycle and its application to a real-world scenario.
- Design a basic DevOps workflow for an online education application.
- Use Git and GitHub for version control.
- Automate application deployment using Ansible.
- Validate deployment using automated checks.
- Document the deployment process and demonstrate the results.

## 3. Selected Real-World Scenario

**Domain:** Online Education

**Application:** EduTrack – Student Learning Dashboard

Students often need to manage assignments, examination preparation, project work, and deadlines. EduTrack provides a centralized dashboard for organizing study activities and tracking task completion.

### Application Features

- Add, edit, complete, and delete study tasks.
- Assign subjects, priorities, task types, and due dates.
- Search tasks and filter them by status.
- Identify overdue tasks.
- View task statistics and overall completion progress.
- View subject-wise learning progress.
- Export task data as a JSON file.
- Save task data in browser local storage.
- Use a responsive interface on desktop and mobile devices.

**Note:** This is a frontend demonstration application. It does not currently include a backend API, centralized database, or multi-user authentication.

## 4. Technology Stack

| Technology | Purpose |
|---|---|
| HTML5 | Application structure |
| CSS3 | Styling and responsive layout |
| JavaScript | Application functionality |
| Git | Version control |
| GitHub | Source code hosting |
| Linux (Ubuntu/WSL) | Execution environment |
| Ansible | Configuration management and deployment automation |
| Python 3 | Runtime support for Ansible |
| HTTP server | Local testing of the deployed website |

## 5. DevOps Lifecycle

### 5.1 Plan

Identify the student task management problem, define application features, and establish deployment requirements.

### 5.2 Develop

Build the EduTrack interface using HTML, CSS, and JavaScript. Implement task management, filtering, progress statistics, and browser-based data persistence.

### 5.3 Version Control

Use Git to track changes and GitHub to maintain the project repository.

Repository: https://github.com/KulshreeNakshane1905/DevOps-Case-Study-Ansible-Automation-Assignment

### 5.4 Test

Perform the following checks:

- Validate the Ansible playbook syntax.
- Verify Ansible connectivity to the local managed host.
- Execute the playbook and inspect the result.
- Confirm that the deployed HTML file exists and is not empty.
- Open the deployed application in a browser and test its features.

### 5.5 Deploy

Use Ansible to create the application directory, copy the HTML file, and verify the deployed file.

### 5.6 Monitor and Maintain

Inspect Ansible execution results, review application behavior, and update the source code when improvements are needed.

For this demonstration, monitoring consists of deployment verification and manual browser testing. Production monitoring, centralized logging, and automated alerts are not implemented.

## 6. System Architecture

The project follows a simple local deployment architecture.

```text
Developer
    |
    v
HTML, CSS and JavaScript
    |
    v
Git and GitHub
    |
    v
Ansible Playbook
    |
    v
Local Linux Environment
    |
    v
/tmp/ansible-webapp/index.html
    |
    v
Python HTTP Server
    |
    v
Web Browser
```

Ansible runs locally and configures the local machine as its managed host. The playbook copies the application to `/tmp/ansible-webapp/`. A Python HTTP server can then serve the deployed HTML file for browser testing.

## 7. Project Structure

```text
devops-ansible-assignment/
├── files/
│   └── index.html
├── screenshots/
├── inventory.ini
├── ansible.cfg
├── playbook.yml
└── README.md
```

- `files/index.html`: EduTrack application source.
- `screenshots/`: Evidence of commands, deployment, and application execution.
- `inventory.ini`: Defines the Ansible managed host.
- `ansible.cfg`: Contains project-level Ansible configuration.
- `playbook.yml`: Automates deployment and verification.
- `README.md`: Project documentation.

## 8. Ansible Configuration

### Inventory

The inventory defines the local machine as the managed host.

```ini
[webservers]
localhost ansible_connection=local ansible_python_interpreter=/usr/bin/python3
```

### Ansible Configuration

```ini
[defaults]
inventory = ./inventory.ini
host_key_checking = True
retry_files_enabled = False
```

### Playbook

The playbook performs the following tasks:

1. Gather system information.
2. Create `/tmp/ansible-webapp/` with appropriate permissions.
3. Copy `files/index.html` to the deployment directory.
4. Check that the deployed file exists.
5. Verify that the destination is a regular, non-empty file.
6. Report successful deployment when the checks pass.

The playbook uses Ansible built-in modules such as `file`, `copy`, `stat`, and `assert`.

## 9. Installation and Execution

### Prerequisites

- Ubuntu Linux or Ubuntu through WSL.
- Python 3.
- Ansible.
- Git.
- A web browser.

### Verify the installation

```bash
python3 --version
ansible --version
git --version
```

### Validate the playbook

From the project directory, run:

```bash
cd ~/devops-ansible-assignment
ansible-playbook --syntax-check playbook.yml
```

### Test Ansible connectivity

```bash
ansible webservers -m ping
```

### Deploy the application

```bash
ansible-playbook playbook.yml
```

### Verify the deployed file

```bash
ls -l /tmp/ansible-webapp/index.html
grep -n "EduTrack" /tmp/ansible-webapp/index.html
```

### Run the website locally

```bash
python3 -m http.server 8000 --directory /tmp/ansible-webapp
```

Open the following URL in your browser:

http://localhost:8000

Stop the HTTP server with `Ctrl+C` when finished.

## 10. Testing and Validation

| Test | Command or Method | Expected Result |
|---|---|---|
| Ansible installation | `ansible --version` | Version information displayed |
| Connectivity | `ansible webservers -m ping` | Successful ping response |
| Syntax validation | `ansible-playbook --syntax-check playbook.yml` | Syntax check succeeds |
| Deployment | `ansible-playbook playbook.yml` | Playbook completes successfully |
| File verification | `ls -l /tmp/ansible-webapp/index.html` | Deployed file exists |
| Browser test | Open `http://localhost:8000` | EduTrack dashboard loads |
| Functional test | Add and complete a task | Task list and progress update |

Record the actual results of each test before submitting the assignment.

## 11. Benefits of Ansible Automation

- **Consistency:** The same deployment steps can be repeated.
- **Automation:** Reduces manual file-copying and configuration work.
- **Validation:** Checks that the application was deployed correctly.
- **Maintainability:** Keeps deployment instructions in a version-controlled playbook.
- **Reproducibility:** Makes it easier to repeat the setup in another suitable environment.
- **Efficiency:** Reduces repetitive deployment tasks.

## 12. Limitations and Future Enhancements

### Current Limitations

- Deployment targets the local Linux machine rather than a remote production server.
- The application uses browser local storage rather than a centralized database.
- There is no automated CI/CD pipeline.
- Monitoring is limited to Ansible output and manual browser testing.
- HTTPS, authentication, and production hosting are not configured.

### Future Enhancements

- Deploy the application to a remote Linux server.
- Configure Nginx using Ansible.
- Add automated HTML and JavaScript testing.
- Integrate GitHub Actions for continuous integration and deployment.
- Add a backend API and database.
- Introduce centralized logging, monitoring, and alerting.
- Deploy the application using Docker and a cloud platform.

## 13. Screenshots and Evidence

Include the following screenshots in the `screenshots/` directory:

1. Ansible version and installation.
2. Ansible connectivity test showing a successful response.
3. Successful playbook syntax validation.
4. Playbook execution recap showing `failed=0`.
5. Verification of the deployed HTML file.
6. EduTrack dashboard running in the browser.
7. GitHub repository showing the project files.


## 14. Conclusion

This project demonstrates a basic DevOps workflow for an online education application. EduTrack provides student task management features, while Git and GitHub support version control and Ansible automates application deployment and verification.

The project illustrates how configuration management can improve deployment consistency, reduce repetitive manual tasks, and make a basic application easier to deploy and maintain. It also provides a foundation for future improvements involving remote servers, automated testing, CI/CD pipelines, and production monitoring.

---

**Project:** DevOps Case Study – Ansible Automation  
**Application:** EduTrack Student Learning Dashboard  
**Repository:** [DevOps-Case-Study-Ansible-Automation-Assignment](https://github.com/KulshreeNakshane1905/DevOps-Case-Study-Ansible-Automation-Assignment)
