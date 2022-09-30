# Create-Local-Yum-DNF-Repository-on-RHEL-9
How to Create Local Yum/DNF Repository on RHEL 9. This will help us to use Redhat without subscription to install packages.

## Prerequisites for creating local Yum/DNF repository
   1. Minimal Install RHEL 9 system
   2. Sudo User with admin privileges
   3. RHEL 9 DVD or ISO file

## 1. Download VM

   1. Download a VM and install Redhat Linux Enterprise 9 on. Ensure that either workspace or GUI is used. Don't use the Redhat server. The reason is             because we will need to download a disk image in our virtual machine
   2. Download the Redhat Enterprise disk image 

## 2. Mount RHEL ISO File or DVD 

We are assuming RHEL 9 iso file is downloaded to the system. Run following mount command to mount ISO file on `/opt/repo` folder.
  
                          sudo mkdir /var/repo
                
                          sudo mount -o loop rhel-baseos-9.0-x86_64-dvd.iso /var/repo/
                          
Note If it is dvd, then run:

                          sudo mount /dev/sr0 /var/repo/
                          
## 3. Next Create Repo File in ‘/etc/yum.repos.d/’ Directory

   1. Next step is to create a repo file with name ‘rhel9-local.repo’ under the folder /etc/yum.repos.d/

                          sudo vi /etc/yum.repos.d/rhel9-local.repo
                          
   2. Next we will paste the following command into the the file then save and close the file.
      
                          [Local-BaseOS]
                          name=Red Hat Enterprise Linux 9 - BaseOS
                          metadata_expire=-1
                          gpgcheck=1
                          enabled=1
                          baseurl=file:///var/repo//BaseOS/
                          gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release

                          [Local-AppStream]
                          name=Red Hat Enterprise Linux 9 - AppStream
                          metadata_expire=-1
                          gpgcheck=1
                          enabled=1
                          baseurl=file:///var/repo//AppStream/
                          gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release   
                          
                          
## 4. Flush Yum/DNF & Subscription Manager Cache          

   Next, We execute following commands to clean yum or dnf and subscription manager cache.
   
                           sudo dnf clean all
                           
                           sudo subscription-manager clean
                          
Note: The output of the above command will give a warning message saying ‘This system is not registered with an entitlement’. In other to suppress this warning message, edit the file  ‘/etc/yum/pluginconf.d/subscription-manager.conf’ , change the parameter ‘enabled=1’ to ‘enabled=0’. Then save and close th file.

                           sudo vi /etc/yum/pluginconf.d/subscription-manager.conf
                           
## 5. Install Packages using Local Repository    

Now we can test our local repository. Run beneath command to view configure repository.

                           sudo dnf repolist
                           
                           sudo dnf install nfs-utils
                           
                           sudo yum update 
                                               
                 
