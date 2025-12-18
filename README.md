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


