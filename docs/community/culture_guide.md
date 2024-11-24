# Zoey's Homelab Culture Guide

!!! note
    This document was originally written by **[Zoey](https://github.com/zekesonxx)**, all credit goes to her for the idea and creation of the source material for this page.

1. [Don't *just* say hello](https://nohello.net/en/)
2. [Don't ask to ask](https://dontasktoask.com/)
3. [Don't use UNRAID](https://en0.sh/raw/xtreks-unraid-rant)
4. [Ask for help with what you want to actually do](https://xyproblem.info/), not a piece of the puzzle you think will get you there.
5. `#offtopic` is 80% shitposting. `#general` and `#general_deux` are 20% shitposting. Learn to distinguish the shitposting from actual advice.
6. **We are not a replacement for googling / looking things up**. We're happy to point you in the right direction, but if you want something that can be easily found online, you're getting linked to LMGTFY/LMDDGTFY.  
Bad question example: "[What's the difference between Docker and VMs?](https://lmddgtfy.net/?q=docker%20vs%20VMs)"
7. **Everyone has their own opinions about what's good and what's bad**. [Human subcultures are nested fractally. There's no bottom](https://xkcd.com/1095/). You've found a fractal nest of bored sysadmins arguing about tech.
8. **Don't come asking "what should I do with my homelab?".** That's a question only you can answer. Homelab is a freeform concept, not a linear adventure or a skill tree. If you don't know what to do in your homelab, the answer might be that it's finished for now and doesn't need anything new.
9. **Budget always matters**. Don't forget to factor in the value of your time as well. Homelabs are an endless time and money pit, there's no limit to how much you can waste on one.
10. **Power cost always matters too**. Cheap power lets you use older systems and less efficient setups. Expensive power means you need to optimize for power draw too. Most people will give advice based on *their* power costs, not yours.
11. [Don't run a summerhost](https://grumpy.systems/2023/please-dont-sell-space-in-your-homelab/). We won't help you if you do, and will actively make fun of you if you insist on doing so, and you *will* deserve the mockery.  
If you decide to anyways, I hope you have a good lawyer on retainer.
12. **We are not paid support staff**. We will mock you if you repeatedly ask dumb questions. Don't come asking to pay for support either, this is what many of us actually do for our jobs, and you're not paying high enough for our rates.

## Server Help

1. **Homelab resource demands aren't actually that high**. 95% of the people in this chat could have all of their needs happily met by a single powerful server, which would be more power efficient and easier to manage than any sort of cluster. 70% of the people in this chat can have that box be a single workstation from 2016 and still have more than enough resources.
2. **Recognize when people are talking at the wrong scale**. Mixed speed L2s are fine for a basic homelab. 10G switches that can't route are fine. You don't need a ceph cluster. ECMP/VRRP is overkill for a homelab.
3. **Servers serve a purpose**. If you come asking about what you should buy or what server is best, our followup question will always be "*for what purpose? what are you doing with it?*"
4. **Raspberry Pis don't make good servers** They're ARM SBCs that like corrupting their microSD cards and frankly just aren't that powerful. A desktop computer from 2014 has more compute power, will draw maybe twice the electricity (so, like 40W max), be way easier to work with, and doesn't involve trying to snipe one from a scalper.

## Quick Takes

* Enterprise wifi at home: TP-Link Omada, HPE Aruba, Ubiquiti Unifi
* Self-contained all in one **wifi** router: Asuswrt device flashed with [asuswrt-merlin](https://www.asuswrt-merlin.net/)
* Self-contained router **without wifi**: spare old PC running pfSense/OPNsense/OpenWRT/VyOS
* Storage OS: TrueNAS Scale (not Core), Proxmox, a plain Debian install with LVM or ZFS and Samba
* Hypervisor: Proxmox or ESXi
* **Why do so many of us hate Ubuntu?** Because it's Debian but way worse because Canonical (the company who makes Ubuntu) is stupid. Run Debian stable or sid instead.

## ZFS Disclaimer

ZFS is a great filesystem, and the majority of us run it somewhere in our homelab.  
**However**, if you have an HDD array, and you want to throw an SSD or two at it to make it faster, stop now.

Using SSDs to speed up a ZFS HDD array basically isn't a thing. If you read online, you'll find mention of two methods:

* **ZIL** only applies to synchronous writes (nearly all writes aren't), and can make your performance *worse*, not better  
(plus it reduces your redundancy/durability against device failure to your ZIL devices)
* **L2ARC** only applies to reads, and takes up a ton of ARC space to keep track of what it in the L2ARC, making your performance *worse*, not better

These two features offer great advantages for the right purposes, like Ceph. However, if you don't already know what they do and that you want them, you don't want them.

If you're running a ZFS HDD array, buy more RAM, not SSDs.  
*Alternatively*, do buy SSDs, but make a separate SSD array and migrate workloads to it

## Ramstik's "How Not to Homelab" MASTERCLASS

*This section written by **Ram "Cloudflare Shill" Stick**, and not by Zoey*

In 4 easy steps you'll learn how to be a complete waste of our time ensuring you'll never be welcomed back!

It's so easy, a caveman could do it!

Join the server looking for advice  
Gatekeep people and their experience  
Mouth off at a mod trying to control the situation  
Insult two mods in timeout

## List of Homelab Conversations

(this section is a WIP)

1. "How do I silence this very loud server not designed to be silenced?"
2. "Help me convince myself that I didn't buy ewaste? I will not accept any argument otherwise."
3. "How do I pirate media?"
