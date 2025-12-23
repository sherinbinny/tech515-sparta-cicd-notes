# **Jenkins Job 2 – Automated Merge (`sherin-job2-ci-merge`)**


## **1. Objective / Why**

The purpose of Job 2 is to automate the process of merging the `dev` branch into the `main` branch after ensuring that all CI tests on Job 1 pass. This is important because:

* It ensures only tested, stable code reaches the `main` branch.
* Reduces manual intervention and human error in merging.
* Demonstrates the integration of continuous integration (CI) and continuous deployment (CD) concepts.

**Screenshot:** *(Job overview screenshot placeholder)*

---

## **2. How I Approached It**

1. **Understanding the flow**: I analyzed Job 1’s behavior, it runs tests on `dev` whenever changes are pushed.
2. **Determining dependencies**: Job 2 should only run after Job 1 passes.
3. **Choosing the right tools/plugins**: I used the **Git Publisher plugin** for merging and pushing, since freestyle jobs don’t have native merge options.
4. **Planning the branch strategy**: Ensured that `dev` and `main` were aligned to avoid non-fast-forward issues.

---

## **3. Steps I Took / What I Did**

### **Step 1: SCM Configuration**

* Repository: `git@github.com:sherinbinny/tech515-test-app-cicd.git`
* Credentials: `sherin-jenkins-2-github-key` (Read/Write)
* Branch Specifier: `main`
* Additional Behavior – Merge Before Build: Merge `dev` into `main` before building

**Why:** Ensures the workspace has combined code before build and push.

**Screenshot:** *(SCM + Merge Before Build config)*

---

### **Step 2: Build Triggers**

* Configured Job 2 to trigger **after Job 1 succeeds**.
* Watched project: `sherin-sparta-app-job1-ci-test`

**Why:** Guarantees that only tested code is merged into `main`.

**Screenshot:** *(Build triggers section)*

---

### **Step 3: Post-Build Actions – Git Publisher**

* Enabled “Push Only If Build Succeeds”
* Enabled “Merge Results”
* Branch to push: `main`
* Target remote: `origin`

**Why:** Automates the merge and ensures that only successfully built code reaches GitHub.

**Screenshot:** *(Git Publisher section)*

---

### **Step 4: Testing the Flow**

* Pushed a change to `dev`.
* Verified Job 1 ran and passed.
* Job 2 triggered automatically.
* Checked console output to confirm `dev` was merged into `main` successfully.
* Verified GitHub `main` branch was updated.

**Screenshot:** *(Console output / GitHub commit history)*

---

## **4. Challenges / What I Learned**

* **Merge conflicts**: Initially Job 2 failed due to conflicts in `README.md`.

  * Solution: Cleaned up branches locally, ensured `dev` and `main` were aligned.
* **Plugin limitations**: Git Publisher cannot resolve merge conflicts automatically, freestyle jobs require clean fast-forward merges.
* **Branch management**: Learned the importance of keeping `dev` in sync with `main` in a CI/CD pipeline.
* **CI/CD best practices**: Learned how to chain Jenkins jobs and enforce quality gates.

---

## **5. Reflections / Why It Matters**

This exercise reinforced the value of:

* Automating repetitive tasks (merges, pushes) safely.
* Understanding the limitations of tools and knowing when manual intervention is needed.
* Integrating CI and CD to maintain code quality and reduce errors.