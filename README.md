# THIS DOCUMENT IS INCOMPLETE AND UNVERIFIED. IT ONLY CONTAINS MY NOTES

# usbip
Configs and instructions for usbip on various platforms combined with using a raspberry pi for switching

## Installation. 
* prerequisites
  * ssh server configured and set up to use key authentication
* install the package
  * see commands below for examples
* configure server device
* configure client
* testing
### Arch
install package

    sudo pacman -S usbip
### Debian
install package

    sudo apt install usbip
    sudo modprobe vhci-hcd
    
    # copy systemd/usbipd.service to/ et /systemd/system/usbipd.service
    sudo systemctl enable usbipd.service
    sudo systemctl start usbipd.service
    # verify everything went as expected
    sudo systemctl status usbipd.service
    
    # allow usbip command to be used without entering a password
    sudo visudo
    
    # append the following g line to the end of the file
    pi ALL=NOPASSWD:/usr/sbin/usbip
    
    # this will still require the sudo command, but it will not prompt for the password. Creating an alias will abstract away the sudo command
    # to do this, edit your .bashrc file and add the following to the alias section
    alias usbip='sudo usbip'
    # then reload the .bashrc file
    source .bashrc 
    
   
### Ubuntu 
install package

    sudo apt install usb-generic-tools
### Windows 
install ssh
configure ssh

    # Run ssh-keygen.exe
    # Copy contents of private key to the file C:\ProgramData\ssh\administrators_authorized_keys
    
    # Configure access rights for C:\ProgramData\ssh\administrators_authorized_keys
    
    $acl = Get-Acl C:\ProgramData\ssh\administrators_authorized_keys 
    $acl.SetAccessRuleProtection($true, $false) 
    $admin = New-Object system.security.accesscontrol.filesystemaccessrule("Administrators","FullControl","Allow") 
    $system = New-Object system.security.accesscontrol.filesystemaccessrule("SYSTEM","FullControl","Allow") $acl.SetAccessRule($admin) 
    $acl.SetAccessRule($system) 
    $acl | Set-Acl
