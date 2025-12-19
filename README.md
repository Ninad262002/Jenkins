## Jenkins Notes

## Jenkins Architecture — Simple Explanation

![Image](https://docs.oracle.com/en/solutions/jenkins-controller-agent-mode/img/jenkins-oci.png?utm_source=chatgpt.com)

![Image](https://media2.dev.to/dynamic/image/width%3D1000%2Cheight%3D420%2Cfit%3Dcover%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fnb3vwtkpjh1gdxgybac7.png?utm_source=chatgpt.com)

![Image](https://media.geeksforgeeks.org/wp-content/uploads/20240312132918/Jenkins-masterSlave.webp?utm_source=chatgpt.com)

### Big Picture (One-line)

👉 **Jenkins has one boss (Controller) and many workers (Nodes).**
The boss decides *what* to do, and the workers actually *do the work*.

---

## 1️⃣ Jenkins Controller (The Brain 🧠)

Think of the **Jenkins Controller** as the **manager of a company**.

It does **management work only**, not heavy tasks.

What the controller does:

* 👤 Manages users (login, permissions)
* 📋 Stores jobs & pipelines
* ⏰ Decides *when* and *where* a job should run
* 🌐 Shows everything in the Jenkins web UI
* 📊 Collects build results (success/failure, logs)

💡 In small setups, the controller can also run jobs itself.
💡 In real companies, **controller is kept clean and safe**, and workers do the actual work.

---

## 2️⃣ Nodes / Agents (The Workers 👷)

**Nodes (Agents)** are the machines that **run your jobs**.

They can be:

* Linux servers
* Windows machines
* MacOS systems
* Docker containers
* Kubernetes pods

What nodes do:

* Run build commands
* Run tests
* Deploy applications

The controller **sends jobs** to these nodes.

---

## 3️⃣ Executors (Hands of the Worker ✋)

An **executor** is like **one worker hand**.

* 1 executor = can run **1 job at a time**
* 2 executors = can run **2 jobs at the same time**

Example:

* A node with **4 executors** can run **4 jobs in parallel**

💡 Usually:

* Small server → fewer executors
* Powerful server → more executors

---

## 4️⃣ How Controller & Nodes Talk

Nodes connect to the controller using:

* 🔐 **SSH** (common for Linux)
* ☕ **JNLP (Java-based)**

This connection lets the controller:

* Assign jobs
* Get logs
* Receive build results

---

## 5️⃣ Tools Live on Nodes, Not Controller 🛠️

Important rule:

> **All build tools are installed on the node, not the controller**

Examples:

* Java, Maven
* Node.js, npm
* Docker
* Python

### Modern Approach (Best Practice)

Instead of installing tools manually:

* 🐳 Use **Docker images** as agents
* ☸️ Use **Kubernetes pods**

✅ Clean environment every time
✅ No dependency conflicts
✅ Easy scaling

---

## 6️⃣ Simple Real-Life Flow Example

1. You create a pipeline in Jenkins UI
2. Controller checks:

   * Which node is free?
   * Which executor is available?
3. Controller sends the job to a node
4. Node runs the job
5. Result goes back to controller
6. You see **SUCCESS ❌ FAILURE** in UI

---

## 7️⃣ Why This Architecture Is Powerful 🚀

* 🔒 Controller stays secure
* ⚡ Jobs run faster (parallel execution)
* 📈 Easy to scale (add more nodes)
* 🤖 Perfect for CI/CD automation

---

### Final One-Line Summary

**Jenkins Controller manages everything, Nodes do the work, Executors run jobs, and Docker/Kubernetes help scale smoothly.**


## Types of Jenkins Projects (Jobs) 

1️⃣ Freestyle Project (Old & Simple)

👉 Best for beginners or very simple tasks

Think of this as:
    “Click buttons → add steps → run one after another”
What it does:
  Pulls code
  Runs tests
  Builds
  Deploys
  (All in a straight line)

Problems:
    Everything is configured using the UI (no code)
    Hard to manage big or complex workflows
    Can’t resume if Jenkins crashes
    Not ideal for modern DevOps pipelines

  📌 Use it when:
     You have a small task or you’re just learning Jenkins.

2️⃣ Pipeline Project (Modern & Recommended)

👉 Best for real-world CI/CD

Here you write your workflow as code using a Jenkinsfile.

Think of it as:
“Write steps in code → Jenkins follows them exactly”
What it supports:
    Stages like Build → Test → Deploy
Conditions (run only if test passes)

Parallel jobs
   Resume if Jenkins restarts

  📌 Use it when:
      You want clean, scalable, production-ready automation.

3️⃣ Multibranch Pipeline Project

👉 Pipeline for multiple Git branches

Instead of creating jobs manually for every branch:
Jenkins scans your repo
Detects branches (main, dev, feature/*)
Runs pipelines automatically for each branch

   📌 Use it when:
      Your team works with many branches.

4️⃣ Maven Project

👉 Special project for Java + Maven
If your project uses Maven:
  Jenkins reads pom.xml
  Runs Maven commands automatically

  📌 Use it when:
      You’re building Java applications with Maven.

5️⃣ Multi-Configuration (Matrix) Project

👉 Same job, multiple environments
Runs the same build with:
Different OS
Different Java versions
Different parameters

Example:
Java 8 + Linux
Java 11 + Linux
Java 17 + Windows

  📌 Use it when:
      You want to test across multiple configurations.

6️⃣ Organization Folder
👉 Just for organizing jobs
This is not a job.
It helps you:
   Group related projects
   Manage many repos/teams easily
 
   📌 Use it when:
       You have many Jenkins jobs and need structure.

| Project Type         | When to Use                |
| -------------------- | -------------------------- |
| Freestyle            | Small, simple tasks        |
| Pipeline             | Modern CI/CD (best choice) |
| Multibranch Pipeline | Multiple Git branches      |
| Maven                | Java + Maven projects      |
| Multi-Configuration  | Test multiple environments |
| Organization Folder  | Organize many jobs         |



