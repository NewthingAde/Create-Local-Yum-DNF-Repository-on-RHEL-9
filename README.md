# Create-Local-Yum-DNF-Repository-on-RHEL-9
How to Create Local Yum/DNF Repository on RHEL 9. This will help us to use Redhat without subscription to install packages.

## Prerequisites for creating local Yum/DNF repository
  1. Minimal Install RHEL 9 system
  2. Sudo User with admin privileges
  3. RHEL 9 DVD or ISO file

## 1. Download VM

Download a VM and install Redhat Linux Enterprise 9 on. Ensure that either workspace or GUI is used. Don't use the Redhat server. The reason is because 

## 2. Mount RHEL ISO File or DVD 

We are assuming RHEL 9 iso file is already copied into the system. Run following mount command to mount ISO file on `/opt/repo` folder.
  


