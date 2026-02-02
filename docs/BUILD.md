sudo apt update
sudo apt install -y busybox-static nano xorriso isolinux syslinux-common qemu-system-x86
nano build_brodylinux.sh
copy the code
chmod +x build_brodylinux.sh
sudo ./build_brodylinux.sh
qemu-system-x86_64 -m 512 -cdrom brodylinux.iso



You can replace the name in the code itself and in the file creation

