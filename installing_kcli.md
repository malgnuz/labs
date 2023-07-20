# Installing KCLI on top of RHEL

## For RHEL 8

1. Enable required repositories
```
subscription-manager repos --disable='*'
subscription-manager repos \
--enable=rhel-8-for-x86_64-baseos-rpms \
--enable=rhel-8-for-x86_64-appstream-rpms \
--enable=fast-datapath-for-rhel-8-x86_64-rpms
```

2. Setup Hypervisor requirements

```
dnf -y install openvswitch3.1 libvirt libvirt-daemon-driver-qemu qemu-kvm cockpit firewalld
usermod -aG qemu,libvirt $(id -un)
newgrp libvirt
systemctl enable --now libvirtd
systemctl enable cockpit.socket --now
systemctl enable firewalld --now
```

3. Managing Virtual Machines through Cockpit

```
dnf -y install cockpit-machines && dnf -y update && reboot
```

4. Installing KCLI

```
curl https://raw.githubusercontent.com/karmab/kcli/main/install.sh | sudo bash
```

5. Configuring KCLI

```
kcli create host kvm -H 127.0.0.1 local
kcli create pool -p /var/lib/libvirt/images default
setfacl -m u:$(id -un):rwx /var/lib/libvirt/images
```

7. Starting with KCLI

List the Cloud images available:

```
kcli list available-images
```

Download a particular Cloud image:

```
kcli download image <IMAGE>

```


## For RHEL 9

1. Enable required repositories
```
subscription-manager repos --disable='*'
subscription-manager repos \
--enable=rhel-9-for-x86_64-baseos-rpms \
--enable=rhel-9-for-x86_64-appstream-rpms \
--enable=fast-datapath-for-rhel-9-x86_64-rpms
```

2. Setup Hypervisor requirements

```
dnf -y install openvswitch3.1 libvirt libvirt-daemon-driver-qemu qemu-kvm cockpit firewalld
usermod -aG qemu,libvirt $(id -un)
newgrp libvirt
systemctl enable --now libvirtd
systemctl enable cockpit.socket --now
systemctl enable firewalld --now
```

3. Managing Virtual Machines through Cockpit

```
dnf -y install cockpit-machines && reboot
```

4. Installing KCLI

```
curl https://raw.githubusercontent.com/karmab/kcli/main/install.sh | sudo bash
```

5. Configuring KCLI

```
kcli create host kvm -H 127.0.0.1 local
kcli create pool -p /var/lib/libvirt/images default
setfacl -m u:$(id -un):rwx /var/lib/libvirt/images
```

7. Starting with KCLI

List the Cloud images available:

```
kcli list available-images
```

Download a particular Cloud image:

```
kcli download image <IMAGE>

```
