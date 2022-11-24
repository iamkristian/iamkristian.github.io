---
layout: post
title:  "Vagrant synced directories"
date:   2016-07-08 07:00
image: IMG_6488.png
image_thumb: IMG_6488_thumb.png
subtitle: The one about vagrant and synced directories
categories: vagrant synced dirs
---
I've often been wanting to mount a dir on the host system, when spinning up a
vagrant server.

Here is how I did it. First I had to install the ``` vagrant-vbguest ``` plugin. With this one liner

```bash
vagrant plugin install vagrant-vbguest
```

Then I added this to my ``` Vagrantfile ```

```bash
Vagrant.configure("2") do |config|
 config.vm.synced_folder "tmp/", "/opt/tmp", owner: "root", group: "root"
end
```

and did a ``` vagrant reload ``` and presto - vagrant mounted the ``` tmp ```
folder inside ``` /opt/tmp ```

