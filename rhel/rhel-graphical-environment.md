## For RHEL >= 7

1. Install the rpms that provide graphical features:

```dnf -y install groupinstall "Server with GUI"```

2. Set the graphical environment as the default target

```systemctl set-default graphical.target```

3. To switch immediately to the graphical environment:

```systemctl isolate graphical.target```
