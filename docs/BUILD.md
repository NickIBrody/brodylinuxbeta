# How to Build and Test

```bash
git clone https://github.com/NickIBrody/brodylinuxbeta.git
cd brodylinuxbeta
chmod +x build.sh
./build.sh
# After build → test in QEMU:
qemu-system-x86_64 -cdrom brodylinux.iso -m 512
Or download pre-built ISO
