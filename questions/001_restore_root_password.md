# Restore root password
It can be preliminary task for starting Your exam. It is crucial to know this procedure by heart.

## Question:
You do not know the root password but You have physical access to the machine. Create new root password and log into the system.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

## Answer:
1. During boot time, when GRUB loader screen is presented, press `e` key. That will open an editor with current kernel boot options. Find the line starting with `linux`. At the end of that line add the `rd.break` parameter and press `Ctrl + x` to continue booting the system with the new kernel options.
2. Type `mount -o remount,rw /sysroot`. This actually gets You RW access to the filesystem. `/sysroot` folder is your filesystem's root.
3. Type `chroot /sysroot` to make this folder new root directory.
4. Now it's time to change the root password (that's why we're here for, right?). Type `passwd` and provide a new password (Just use "redhat", to not forget).
5. In order to finish the task, SELinux must be taken care of. If not, contents of `/etc/shadow` will be messed up. Create `/.autorelabel` which will force a relabel on the next boot: `touch /.autorelabel`
6. Type `exit` **twice** (with pressing ENTER after each one. Once for the root jail, another for ). This will continue the booting process, performing the autorelabel.
7. Now You can log into the system using new password

## Additional comment:
It is possible to edit startup parameters of the kernel from the command line and make it persistent. For legacy BIOS systems, edit `/etc/default/grub` file and after that make sure to run `grub2-mkconfig > /boot/grub2/grub.cfg` in order to apply the changes. For the UEFI systems, the file is `/boot/efi/EFI/redhat/grub.cfg`.

This process only works for GRUB and GRUB-like bootloaders.

Keep this process near your heart.
