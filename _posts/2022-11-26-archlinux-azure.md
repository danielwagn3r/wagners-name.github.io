---
layout: post
title:  Arch Linux on Azure
date:   2022-11-26 14:10:00 +0100
category: linux
tags:   archlinux azure cloud image
---
[![Arch Linux on Azure](/images/20221126/archlinux01.webp)](https://archlinux.org)

After years of using my favorite Linux distribution on my on-premise systems, like desktops, servers or even Raspberry Pis I've be always keen to use Arch on cloud as well. Unfortunately there aren't any prebuilt images for Arch Linux available on the most public hyperscalers.

I'm now happy to announce the availabilty of an community Arch Linux image on Azure, as I got the possibility to be party of the preview of the community galleries preview [^2].

You can find the image using the *Community Images (PREVIEW)* option on Azure Portal:

[![Community Images](/images/20221126/archlinux03.webp)](https://portal.azure.com/#create/Microsoft.VirtualMachine)

## Building the image

After reading some blog posts and articles [^1],[^5],[^6],[^7] on the topic, I experimented with the image generation on my own. After some initial failes with QEMU and due the possiblity of a Windows box with Hyper-V on it I choose that approach to bootstrap my image. Initally I even skipped `cloud-init` on only packaged the `waagent` in the image, but I soon saw that the handling of an `cloud-init` enabled image was by far smoother when on Azure.

On the portal this then looks like this:

![Virtual machine properties](/images/20221126/archlinux02.webp)

The images is provided as is without any guarantee or liability.

## Upcoming work

Currently the image only support generation 1 VMs on Azure. Support for generation 2 VMs [^3] would be nice, but requires some work with Secure Boot. Azure enables trusted launch [^4] per default with generation two VMs.

Another interesting option would be to provide an ARM based image, as Azure VMs with Arm are GA since September this year [^8]

In case anybody want's to help with the work on this, just drop me a note.

## References

[^1]: [https://learn.microsoft.com/en-us/azure/virtual-machines/linux/imaging](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/imaging)
[^2]: [https://learn.microsoft.com/en-us/azure/virtual-machines/share-gallery-community](https://learn.microsoft.com/en-us/azure/virtual-machines/share-gallery-community)
[^3]: [https://learn.microsoft.com/en-us/azure/virtual-machines/generation-2](https://learn.microsoft.com/en-us/azure/virtual-machines/generation-2)
[^4]: [https://learn.microsoft.com/en-us/azure/virtual-machines/trusted-launch](https://learn.microsoft.com/en-us/azure/virtual-machines/trusted-launch)

[^5]: [https://guyrobottv.wordpress.com/2019/01/17/running-arch-linux-on-microsoft-azure-in-2019/](https://guyrobottv.wordpress.com/2019/01/17/running-arch-linux-on-microsoft-azure-in-2019/)
[^6]: [https://codito.in/archlinux-on-azure/](https://codito.in/archlinux-on-azure/)
[^7]: [https://gist.github.com/z3ntu/e2750efd7f0b93ab3427f097de3fbefa](https://gist.github.com/z3ntu/e2750efd7f0b93ab3427f097de3fbefa)
[^8]: [https://azure.microsoft.com/en-us/blog/azure-virtual-machines-with-ampere-altra-arm-based-processors-generally-available/](https://azure.microsoft.com/en-us/blog/azure-virtual-machines-with-ampere-altra-arm-based-processors-generally-available)