-> RockLinux in WSL2 -> https://github.com/rocky-linux/sig-cloud-instance-images

-> Make Download of image from this link -> https://github.com/rocky-linux/sig-cloud-instance-images/blob/Rocky-8.5-x86_64/rocky-8.5-docker-x86_64.tar.xz

-> Now create a directory to us install our Rocky Linux in WSl2

mkdir $HOME\wsl\rockylinux

-> Change .tar file name to rocky-linux-rootfs.tar

-> Set the ws2 version as default

wsl --set-default-version 2

-> Now import image

wsl --import rocky $HOME\wsl\rockylinux $HOME\Downloads\rocky-linux-rootfs.tar

-> To start the linux image run command below:

wsl -d rocky

-> After make login with root run command  to upgrade the distro

dnf upgrade

-> Now we will install tools to create own user

dnf install -y passwd cracklib-dicts

-> Command to create the user

useradd -G wheel rocketman

-> Command to give a password to own user

passwd rocketman / roketto

-> Install some things before proced with ouwn user
dnf install sudo
dnf install ncurses
dnf install htop grep procps-ng
dnf install procps-ng

-> Make login with ouwn user

wsl -d rocky -u rocketman

-> Get the Id to us insert in register key to define own user as default
id -u

-> Get number of command above, and run the command below in Poweshell with adm level.

Get-ItemProperty Registry::HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Lxss\*\ DistributionName | Where-Object -Property DistributionName -eq rocky  | Set-ItemProperty -Name DefaultUid -Value 1000

Close and reopne wsl2 of RockyLInux, now you can see that we are logged with own user

Well done, now we need make some configuration to use command ps, grep and others