This is an development and test environment prototype which also allows user to deploy new version of application to Kubernetes after testing with Gitlab CI features. It uses docker in docker concept to prepare docker containers and test.


# How to install

Requirements:
- Docker installed ubuntu machine
- ansible
- curl
- git client
- DockerHub Account
- /srv/gitlab-runner/config/ folder to share secret credentials with stack

# Installation


```

mkdir -p /srv/gitlab-runner/config/; echo "YOUR_DOCKERHUB_PASSWORD" > /srv/gitlab-runner/config/SECRET_DOCKERHUB_PASSWORD

# Option 1 (Clone my example repository which is at git clone https://github.com/enisozgen/flask-with-test.git)
ansible-playbook playbook.yml # and follow the instructions of command output.

# Option 2 (Show your own public repository)
ansible-playbook -e repopath=/path/of/cloned/folder playbook.yml # and follow the instructions of command output.
```

- Installation provides you Gitlab server and Gitlab Runner in your local machine and allows you to experience CI development and CI deployment to the Kubernetes environment.

Normally, ansible automations should work with one-run but Gitlab does not provide TOKEN via API. It's necessary to login to `http://YOUR_URL:8080/root/flask-with-test/-/settings/ci_cd` with **user:root password:password** paste the runner token to command line.


# File Structure

```
.
├── ansible.cfg
├── blueprints
│   ├── gitlab-ci-permissions.yml  # Namespace and app permissions file
│   ├── gitlab-runner.yml          # Gitlab runner configuration
│   └── gitlab-server.yml          # Gitlab server configuration
├── playbook.yml                   # Main ansible playbook
├── roles                          # Ansible roles
│   ├── deploy-gitlab
│   └── install-k3s
└── runner                         # Some basic changes for gitlab Runner
    └── Dockerfile
```

# Usage

After registration you can see necessary CI pipeline at http://YOUR_URL:8080/root/flask-with-test/-/pipelines

After some change in repository you can deploy new version of your application.

```
git push --set-upstream http://root:password@YOUR_URL:8080/root/flask-with-test.git master
```

# Uninstall

By using the command at below you can stop all processes.

`k3s-killall.sh ; k3s-uninstall.sh`
