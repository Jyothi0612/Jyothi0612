# 👋 Hi, I'm Siva Jyothi Pamarthy

### DevOps Engineer in the making | Linux | Shell | Ansible | Terraform | AWS

Software engineer in Stockholm moving from frontend into **DevOps**. I shipped production web apps for 8 years, the last 4 on a regulated online gaming platform (5 brands, 6 licensed markets).

Now I work on the other side of the deploy: **I build servers by hand, automate them, then break them on purpose**, and write down every failure and how I fixed it.

---

## 🛠️ Technical Skills

| Category | Technologies |
|---|---|
| Linux | RHEL 9 / Rocky, Bash, systemd, nginx, cron, SSH |
| Configuration Management | Ansible (playbooks, roles, dynamic inventory) |
| Infrastructure as Code | Terraform (state, variables, provisioners) |
| Cloud | AWS (EC2, Route 53, Security Groups) |
| Containers | Docker, Docker Compose |
| Version Control & CI | Git, GitLab, GitLab CI, GitHub Actions |
| Monitoring | Sentry, journalctl |
| Frontend | TypeScript, Vue, React |
| Learning now | Kubernetes, Prometheus |

---

## 🚀 Featured Projects

**1. [devops-by-breaking](https://github.com/Jyothi0612/devops-by-breaking)**
- 20 break-fix labs named after the error you'd see: "disk full, du says empty", "site returns 502", "pod in CrashLoopBackOff".
- Every lab starts broken on a laptop; a checker proves it was really fixed. CI tests each lab on amd64 + arm64.
- Runtimes: Rocky Linux with systemd, Docker, k3s, Terraform and Ansible.

**2. [Fika Stockholm](https://github.com/Jyothi0612/fika-stockholm)**
- A microservices café-ordering app deployed by hand on 11 RHEL 9 EC2 servers, one per component.
- Route 53 private DNS, security groups that only allow server-to-server traffic, every service under systemd as its own user.
- Shell scripts rebuild any server from zero.

**3. One shop, automated three ways**
- The same 10-service app deployed with shell scripts, then Ansible, then Terraform. Each version fixes what hurt in the one before.
- Shell: [v1](https://github.com/Jyothi0612/shell-roboshop-v1) · [v2](https://github.com/Jyothi0612/shell-roboshop-v2) | Ansible: [v1](https://github.com/Jyothi0612/roboshop-ansible-v1) · [v2](https://github.com/Jyothi0612/roboshop-ansible-v2) · [dynamic inventory](https://github.com/Jyothi0612/ansible-dynamic-inventory) | Terraform: [learn-terraform](https://github.com/Jyothi0612/learn-terraform)

---

## 🔥 Incidents I Debugged

**terraform apply hung, then the server was "tainted"**
`remote-exec` kept retrying SSH and timed out. `nc -z <ip> 22` was open, so not the network. The official RHEL 9 image only allows key login. A failed creation-time provisioner taints the resource, so the next plan replaced it.

**The script worked in my terminal, then cron ran it**
Cron runs with a minimal `PATH`, and it doesn't expand `$PATH` in the crontab. Fix: full paths and logging with `>> /var/log/archive.log 2>&1`. Now I test jobs with `env -i PATH=/usr/bin:/bin /bin/sh -c '…'`.

**tar: "Cannot connect to logs-2026-10-23-02: resolve failed"**
A timestamp from `date +%F-%T` put colons in the file name, and tar reads `name:path` as a remote host. Fix: `date +%Y-%m-%d-%H-%M-%S`.

---

## 📊 GitHub Statistics

<p align="center">
  <img src="https://github-stats-extended.vercel.app/api?username=Jyothi0612&show_icons=true&theme=tokyonight&hide_border=true&cache_seconds=86400&include_all_commits=true" alt="GitHub Statistics" />
</p>

<p align="center">
  <img src="https://github-stats-extended.vercel.app/api/top-langs/?username=Jyothi0612&layout=compact&theme=tokyonight&hide_border=true&cache_seconds=86400" alt="Top Languages" />
</p>

---

## 🐍 GitHub Contributions

<p align="center">
  <img src="https://raw.githubusercontent.com/Jyothi0612/Jyothi0612/output/github-snake-dark.svg" alt="GitHub Contribution Snake" />
</p>

---

## 🔥 GitHub Streak

<p align="center">
  <img src="https://streak-stats.demolab.com?user=Jyothi0612&theme=tokyonight&hide_border=true" alt="GitHub Contribution Streak" />
</p>

---

## 🤝 Connect With Me

<p align="left">
  <a href="https://linkedin.com/in/siva-jyothi-pamarthy-14622547">
    <img src="https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin" alt="LinkedIn"/>
  </a>
  <a href="mailto:jyothipamarthy@gmail.com">
    <img src="https://img.shields.io/badge/Email-Contact-red?style=for-the-badge&logo=gmail" alt="Email"/>
  </a>
  <a href="https://github.com/Jyothi0612">
    <img src="https://img.shields.io/badge/GitHub-Follow-black?style=for-the-badge&logo=github" alt="GitHub"/>
  </a>
</p>

---

**🐧 Linux | ⚙️ Automation | ☁️ AWS | 🔧 Break-fix**

*Open to DevOps, platform and SRE roles in Stockholm, hybrid or remote.*
