---
layout: post
title:  "virtiofs"
date: 2022-12-30 22:04:00 +0700
categories: jekyll update
---

Buat xml memorybacking
```sh
virt-xml <domain> --edit --memorybacking access.mode=shared,source.type=memfd
```
```sh
[root@srv1 ~]# virt-xml domain --edit --memorybacking access.mode=shared,source.type=memfd
Domain 'domain' defined successfully.
Changes will take effect after the domain is fully powered off.
```
Lalu poweroff VM dan start kembali

Selanjutnya buat xml untuk virtiofs
```sh
virt-xml <domain> --build-xml --print-xml --filesystem /mnt/iso/,isoblk,driver.type=virtofs,accessmode=passthrough
```
Output
{% highlight ruby %}
<filesystem accessmode="passthrough" type="mount">
  <source dir="/mnt/iso/"/>
  <target dir="isoblk"/>
  <driver type="virtofs"/>
</filesystem>
{% endhighlight %}

Attach ke live VM dengan perintah berikut
```sh 
virsh attach-device --domain <domain> --file fs.xml  --live
```

Output
```sh
[root@srv1 ~]# virsh attach-device --domain domain --file fs.xml  --live
Device attached successfully
```

