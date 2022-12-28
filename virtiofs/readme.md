buat xml memorybacking
virt-xml <domain> --edit --memorybacking access.mode=shared,source.type=memfd

OUTPUT:
  
[root@srv1 ~]# virt-xml domain --edit --memorybacking access.mode=shared,source.type=memfd
Domain 'cent8-vm1' defined successfully.
Changes will take effect after the domain is fully powered off.

selanjutnya poweroff VM dan start kembali

buat xml untuk virtiofs
  
virt-xml <domain> --build-xml --print-xml --filesystem /mnt/iso/,isoblk,driver.type=virtofs,accessmode=passthrough

OUTPUT:
  
[root@srv1 ~]# virt-xml domain --build-xml --print-xml --filesystem /mnt/iso/,isoblk,driver.type=virtofs,accessmode=passthrough
  
<filesystem accessmode="passthrough" type="mount">
  <source dir="/mnt/iso/"/>
  <target dir="isoblk"/>
  <driver type="virtofs"/>
</filesystem>

attach ke live VM dengan perintah berikut
  
virsh attach-device --domain <domain> --file fs.xml  --live

OUTPUT:
  
[root@srv1 ~]# virsh attach-device --domain domain --file fs.xml  --live

Device attached successfully
