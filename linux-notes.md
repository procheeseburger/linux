# General Config

Commands:
  Change Password:
     # passwd

  Set hostname:
    # nano /etc/hostname

  Set IP:
    # nano /etc/netplan/00

  network:
    version: 2
    renderer: networkd
    ethernets:
    eth0:
    dhcp4: no
    addresses: [192.168.1.222/24]
    gateway4: 192.168.1.1
    nameservers:
    addresses: [1.1.1.1]

  Set Timezone:
    # timedatectl set-timezone America/New_York

  Set Shell:
    # usermod phenom -m -s /bin/bash -c "admin user"

  Set priv:
    # usermod -aG sudo,adm,docker

DNS:

  Commands:
    # sudo rm -f /etc/resolv.conf
    # sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf

    # systemctl restart systemd-resolved
    # systemctl status systemd-resolved

Updates:

    set the unattended update package:
      # sudo apt install unattended-upgrades
      # sudo dpkg-reconfigure --priority=low unattended-upgrades

    view:
      # cd /etc/apt/apt.conf.d/
      # more 20auto-upgrades
      # more 50unatteded-upgrades

    dry run:
      # sudo unattended-upgrade --dry-run --debug

Version:

  Commands:

    Show the current version of linux:
      # cat /etc/*release*

Grep:

  Commands:

    Search for somthing with a "-" in the name:

      # kubectl get pods --all-namespaces | grep "\-master"
    
        Notice the \ before the -

K8s search for syntax:
    - You can search for the syntax you need
    - you can also list out the lines below

  Commands:

    Search for syntax:

      # k explain pods --recursive | less
        / "search"
    
    List specific lines:
      # kubectl explain pods --recursive | grep -a# evnFrom

        you can have grep list the number of lines with -a# so -a8 will stil the 8 lines below

Watch:
    -you can watch a command every 2 seconds

  Commands:
    # watch "kubectl get pods"
    # watch microk8s.kubectl get all --all-namespaces

Scripts:
    -How to run a script

  Commands:
    # ./script.sh

SSL/TLS:

    SSH Key is saved:
        .ssh/

    You will see 2 keys:
        Private: id_#########
        Public:  id_#########.pub

    Send your Public key to a server:
        # ssh-copy-id -i ~/.ssh/id_#######.pub 1.1.1.1

    Specify ssh key:
      # ssh -i ~/.ssh/"keyname" "server name"

MOUNT NFS SHARE:

    Mount:    
      # mount -t nfs -O user=k8s,pass=password 10.10.30.100:/volume1/nfs /mnt 

    Verify mount:
      # mount | grep nfs

    Unmount it:
      # umount /mnt (only do this if this is the only mount)

ZIP / Compress:

    Unzip a .tgz files:
      # tar -xvzf /path/to/yourfile.tgz -C /path/where/to/extract/

Host Files:

    Update Host file with all nodes in cluster:
      # microk8s kubectl get nodes -o wide | awk '{ print $6 " " $1 }' | tail -n +2 | grep -v $(hostname)  >> /etc/hosts

Storage:

    Ubuntu will typically only use 200GB space:

    # lvresize -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv
    # resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv

HELM:

    If Helm is being fucking stupid, try this:
      # ~$ kubectl config view --raw >~/.kube/config

GITHUB:

clone a dir:

    #gcl git@github.com:repo/file 

Namespaces stuck in terminating:

    https://computingforgeeks.com/how-to-force-delete-a-kubernetes-namespace/