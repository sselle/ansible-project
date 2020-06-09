### Used commands: (remote-user, ssh-key, inventory file defined in ansible.cfg)
    ansible aws-vms -a "free -m"
    ansible aws-vms -m ping

### Basic command to run a playbook 
    ansible-playbook playbooks/check-ntp.yaml

### attach disk
    lsblk
    sudo mkfs.ext4 -m 0 -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/[DEVICE_ID]
    sudo mkdir /dss
    sudo chown dssuser /dss
    sudo mount -o discard,defaults /dev/[DEVICE_ID] /dss[MNT_DIR]
    sudo cp /etc/fstab /etc/fstab.backup
    sudo blkid /dev/[DEVICE_ID]
    to fstab >> UUID=[UUID_VALUE] /mnt/disks/[MNT_DIR] ext4 discard,defaults 0 2

### get dss, install deps, install dss