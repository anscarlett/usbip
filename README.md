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
    sudo usbipd -D
    
   
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
