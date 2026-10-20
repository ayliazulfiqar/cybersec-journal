# Day 15 - Project 1, Session 1 (Home Hacking Lab setup)

## What I did today
- Installed VirtualBox on Linux Mint
- Imported the Kali Linux VM and ran updates
- Downloaded and imported Metasploitable 2 (not started yet, set to Host-only)
- Drew the lab diagram and started the project README

## Project link
 [Project 1: Home Hacking Lab](home-lab/README.md)

## What went well

Successfully installed and launched VirtualBox 7.2.20 on Linux Mint 22.3.

Downloaded and booted the Kali Linux virtual machine.

Configured Kali with 2 GB of RAM and 2 CPUs to suit my laptop's 8 GB of RAM.

Created a Host-only network named vboxnet0 for the lab.

Downloaded and extracted Metasploitable 2, my intentionally vulnerable target machine.

Created a lab diagram to document the virtual machines and their network setup.

## Problems I hit

The initial VirtualBox installation failed because of a kernel module build error.

Had difficulty finding the Host-only Network settings in VirtualBox 7.2.20.

Created the vboxnet0 network using the Terminal when I couldn't find the network manager.

Had trouble copying the lab diagram into my project folder because the project folder was on GitHub rather than stored locally on my laptop.

Learned to upload files directly through the GitHub website.


## What I learned

How to configure virtual machines using VirtualBox on Linux Mint.

Why RAM and CPU allocation matter when running virtual machines on a laptop with limited resources.

How to create a Host-only network for communication between virtual machines.

Why intentionally vulnerable machines such as Metasploitable 2 must be isolated from my home network and the internet.

How to use the Terminal to troubleshoot VirtualBox networking issues.

How to document a cybersecurity lab using Markdown and a network diagram.

How to upload project files and diagrams to GitHub.

## Next

Session 2: build the isolated network and test connectivity between Kali and the target
