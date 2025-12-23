# Jenkins CI Job 1 – Testing Stage with Webhook Trigger

## 1. Objective (What)

The objective of this task was to set up **Job 1 of a Continuous Integration (CI) pipeline** using Jenkins.
This job focuses on the **testing stage**, ensuring that automated tests are run every time code is pushed to the GitHub repository.

The key goals were:

- To integrate Jenkins with GitHub
- To trigger builds automatically using a webhook
- To run Node.js application tests as part of CI
- To verify successful builds using Jenkins console output

---

## 2. Tools & Technologies Used (What)

- **Jenkins** (Freestyle project)
- **GitHub** (Source code repository)
- **AWS EC2** (Jenkins host)
- **Node.js v20**
- **npm**
- **GitHub Webhooks**
- **SSH credentials for secure access**

---

## 3. Jenkins Job Configuration (How)

### 3.1 Job Setup

A Jenkins freestyle project named:

**`sherin-sparta-app-job1-ci-test`**

was created with the following configuration:

- Description: Testing stage of CI triggered via webhook
- Maximum builds to keep: 5 (to manage disk usage)

📸 _Screenshot: Jenkins job general configuration_

---

### 3.2 Source Code Management

- Git was selected as the SCM
- Repository URL:

  ```
  git@github.com:sherinbinny/tech515-sparta-test-app-cicd.git
  ```

- Credentials used:
  **sherin-jenkins-2-github-key**
- Branch specifier:

  - Initially tested on `main`
  - Final configuration: `*/dev`

📸 _Screenshot: Source Code Management configuration_

---

### 3.3 Build Trigger Configuration (How & Why)

The option **“GitHub hook trigger for GITScm polling”** was enabled.

This allows Jenkins to start a build **automatically** whenever GitHub sends a webhook notification after a push event, rather than relying on manual builds or scheduled polling.

📸 _Screenshot: Build trigger configuration_

---

### 3.4 Build Environment Setup

- Node & npm binaries were added to the PATH
- Node.js version **20** was selected

This ensures consistency between local development and the CI environment.

📸 _Screenshot: Build environment configuration_

---

### 3.5 Build Steps (Testing Stage)

The following shell commands were added:

```bash
cd app
npm install
npm test
```

These steps:

1. Navigate to the application directory
2. Install required dependencies
3. Run automated tests to validate the application

📸 _Screenshot: Execute shell build step_

---

## 4. GitHub Webhook Setup (How)

A webhook was configured in the GitHub repository with:

- Payload URL pointing to the Jenkins server
- Content type set to `application/json`
- Triggered on push events

This allows GitHub to notify Jenkins instantly whenever code changes are pushed.

📸 _Screenshot: GitHub webhook configuration_

---

## 5. Credentials Configuration (Why)

An SSH key (`sherin-jenkins-2-github-key`) was added to Jenkins credentials to securely authenticate Jenkins with GitHub.

Using SSH credentials is more secure than username/password authentication and is the recommended industry approach for CI/CD pipelines.

📸 _Screenshot: Jenkins credentials configuration_

---

## 6. Build Execution & Verification (What Happened)

- A manual build was triggered initially to verify the configuration
- Jenkins successfully initiated the build on the EC2 instance
- Changes were made to the `README.md` file on both the `main` and `dev` branches
- Each push automatically triggered a new Jenkins build via the webhook
- All builds completed successfully, indicated by a **green status icon**

📸 _Screenshot: Successful Jenkins build (green tick)_
📸 _Screenshot: Console output showing npm test success_

---

## 7. Why This Setup Is Important (Why)

This CI setup ensures:

- Code is automatically tested on every push
- Errors are caught early before deployment
- Developers receive immediate feedback
- Manual testing and human error are reduced

This reflects real-world DevOps practices where automation is critical for speed, reliability, and scalability.

---

## 8. What I Learned (Reflection)

From completing this task, I learned:

- How Jenkins integrates with GitHub using webhooks
- How to configure secure SSH credentials for CI pipelines
- How automated testing fits into the CI lifecycle
- How to debug builds using Jenkins console output
- The importance of consistent environments using Node version control

This task helped me understand how individual CI jobs fit into a larger CI/CD pipeline and reinforced how automation improves software quality and delivery speed.

---

## 9. Conclusion

The Jenkins CI Job 1 was successfully implemented to automate the testing stage of the pipeline.
By using webhooks, secure credentials, and automated tests, the pipeline reliably validates code changes and provides immediate feedback, demonstrating a core principle of Continuous Integration.
