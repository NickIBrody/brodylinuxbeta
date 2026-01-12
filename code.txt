#!/bin/bash
set -e

ISO=brodylinux.iso
WORK=brody_work

echo "[1] clean"
rm -rf $WORK
mkdir -p $WORK/{rootfs,iso/isolinux}

echo "[2] rootfs dirs"
cd $WORK/rootfs
mkdir -p bin sbin etc proc sys dev tmp usr/bin
chmod 1777 tmp

echo "[3] busybox"
cp /bin/busybox bin/
ln -s busybox bin/sh
ln -s busybox bin/ls
ln -s busybox bin/cd

echo "[4] nano"
cp /bin/nano usr/bin/nano
cp -r /usr/share/nano usr/share 2>/dev/null || true

echo "[5] init"
cat > init << 'EOF'
#!/bin/sh
mount -t proc proc /proc
mount -t sysfs sys /sys
mount -t devtmpfs dev /dev

clear
echo "================================"
echo " Welcome to BrodyLinux"
echo " Telegram: @werg23p"
echo "================================"
echo ""

exec /bin/sh
EOF
chmod +x init

echo "[6] initrd"
find . | cpio -o -H newc | gzip > ../initrd.img
cd ..

echo "[7] kernel"
cp /boot/vmlinuz-$(uname -r) iso/vmlinuz
cp initrd.img iso/initrd.img

echo "[8] isolinux"
cp /usr/lib/ISOLINUX/isolinux.bin iso/isolinux/
cp /usr/lib/syslinux/modules/bios/ldlinux.c32 iso/isolinux/

cat > iso/isolinux/isolinux.cfg << 'EOF'
DEFAULT brody
LABEL brody
  KERNEL /vmlinuz
  INITRD /initrd.img
  APPEND init=/init quiet loglevel=0 panic=0
EOF

echo "[9] build iso"
xorriso -as mkisofs \
  -o ../$ISO \
  -b isolinux/isolinux.bin \
  -c isolinux/boot.cat \
  -no-emul-boot \
  -boot-load-size 4 \
  -boot-info-table \
  iso

echo "DONE: $ISO"
