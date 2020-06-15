### Used commands: (remote-user, ssh-key, inventory file defined in ansible.cfg)
    ansible aws-vms -a "free -m"
    ansible aws-vms -m ping

### execute only one fork of the command --> perform each server in sequence
    ansible multi -a "hostname" -f 1

### use the yum module to install sofware (-b: become)
    ansible multi -b -m yum -a "name=chrony state=present"

### use service module 
    ansible multi -b -m service -a "name=chronyd state=started enabled=yes" 

### Basic command to run a playbook 
    ansible-playbook playbooks/check-ntp.yaml

### get / send files to server
    ansible multi -m copy -a "src=/etc/hosts dest=/tmp/hosts"
    ansible multi -b -m fetch -a "src=/etc/hosts dest=/tmp"

### directories, symlinks, files
    ansible multi -m file -a "dest=/tmp/test mode=644 state=directory"
    ansible multi -m file -a "src=/src/file dest=/dest/symlink state=link"
    ansible multi -m file -a "dest=/tmp/test state=absent"

### run job in background for max 3600 seconds
    ansible multi -b -B 3600 -P 0 -a "yum -y update"

### grep needs shell module (native ansible command doesn't work, 
### because it only returns on complete operations )
    ansible multi -b -m shell -a "tail /var/log/messages | grep ansible

### deploy from repo
    ansible app -b -m git -a "repo=git://example.com/path/to/repo.git \
    dest=/opt/myapp update=yes version=1.2.4"

### get dss, install deps, install dss
    wget

### Docker
    sudo yum install -y yum-utils
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    sudo yum install docker-ce docker-ce-cli containerd.io --nobest