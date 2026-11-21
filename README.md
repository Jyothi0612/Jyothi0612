<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner-dark.svg">
  <img src="assets/banner-light.svg" alt="jyothi@stockholm: 8 years frontend in production, now DevOps. I build servers by hand, automate them, then break them on purpose. Open to DevOps, platform and SRE roles in Stockholm." width="100%">
</picture>

[LinkedIn](https://linkedin.com/in/siva-jyothi-pamarthy-14622547) · [Email](mailto:jyothipamarthy@gmail.com) · Stockholm, Sweden

### `$ ls ~/work --sort=proof`

| Repo | What it proves |
|---|---|
| **[devops-by-breaking](https://github.com/Jyothi0612/devops-by-breaking)** | I can debug, and I can design checks. 20 break-fix labs (disk full, 502s, CrashLoopBackOff), each one tested in CI on amd64 + arm64 to start broken and be fixable. |
| **[fika-stockholm](https://github.com/Jyothi0612/fika-stockholm)** | I can run many servers by hand. 11 RHEL 9 EC2 servers, Route 53 private DNS, locked-down security groups, every service its own user under systemd. |
| **one shop, automated 3 ways** | I know *why* we automate. The same 10-service app deployed again and again, each version fixing what hurt in the last one. |

```text
shell-roboshop-v1  ──▶  shell-roboshop-v2  ──▶  roboshop-ansible-v1  ──▶  roboshop-ansible-v2  ──▶  learn-terraform
copy-paste scripts      shared common.sh        one playbook/service      reusable roles            the servers too
```
[shell v1](https://github.com/Jyothi0612/shell-roboshop-v1) · [shell v2](https://github.com/Jyothi0612/shell-roboshop-v2) · [ansible v1](https://github.com/Jyothi0612/roboshop-ansible-v1) · [ansible v2](https://github.com/Jyothi0612/roboshop-ansible-v2) · [dynamic inventory](https://github.com/Jyothi0612/ansible-dynamic-inventory) · [terraform](https://github.com/Jyothi0612/learn-terraform)

### `$ journalctl -p err --since "this year"`

Things that broke on me, written up the way a postmortem would be.

<details>
<summary><b>terraform apply hung for 5 minutes, then the server was "tainted"</b></summary>

- **Symptom:** `remote-exec` retried SSH with a password until it timed out. The next plan said 1 to add, 1 to destroy.
- **Checked:** `nc -z <ip> 22` was open, so it wasn't the network. `ssh -o PreferredAuthentications=none` showed only `publickey` was allowed.
- **Cause:** the official RHEL 9 image turns password login off. The training image had a password.
- **Fix:** an SSH key in the `connection` block.
- **Learned:** if a creation-time provisioner fails, the resource is marked tainted and the next apply replaces it. `terraform apply -replace` does the same on purpose.
</details>

<details>
<summary><b>The script worked in my terminal, then cron ran it</b></summary>

- **Symptom:** the nightly log-archive job never archived anything, but it still exited 0.
- **Cause:** cron runs with `PATH=/usr/bin:/bin`. Writing `PATH=$PATH:...` in a crontab made things worse, because cron doesn't expand variables.
- **Fix:** write `PATH` out in full, use full paths, and log with `>> /var/log/archive.log 2>&1`.
- **Learned:** test a job the way cron runs it: `env -i PATH=/usr/bin:/bin /bin/sh -c '…'`
</details>

<details>
<summary><b>tar: "Cannot connect to logs-2026-10-23-02: resolve failed"</b></summary>

- **Cause:** `date +%F-%T` puts colons in the file name, and tar reads `name:path` as `host:path`.
- **Fix:** `date +%Y-%m-%d-%H-%M-%S`
</details>

### `$ tree ~/stack`

```text
~/stack
├── linux/      RHEL 9 · Rocky · Bash · systemd · nginx · cron · ssh        [built]
├── automate/   Ansible · Terraform                                         [built]
│               Git · GitLab · GitLab CI                                    [production]
├── cloud/      AWS EC2 · Route 53 · security groups                        [built]
│               Docker Compose                                              [production]
├── observe/    Sentry                                                      [production]
│               journalctl                                                  [built]
├── frontend/   TypeScript · Vue                                            [production]
└── next/       Kubernetes · CI/CD pipelines · Prometheus                  [learning]

production = used at work · built = in my own repos · learning = in progress
```

### `$ git log --oneline career`

```text
2026      DevOps on AWS: Linux → shell → Ansible → Terraform, all built by hand first
2021–26   Frontend Developer · online gaming, 5 brands × 6 licensed markets
          live outage hotfix · pen-test XSS fix · Mercurial → Git/GitLab + CI · Docker Compose dev stack
2019–21   career break: moved to Sweden
2014–19   Software Engineer · Hyderabad
```
