# REALTIME-X-SOURCES

Pre-Patched Linux Kernel Sources REALTIME-X

Sunday 21-01-2020. =

Update to 5.4.13 Stable Kernel LTS.

Updated REALTIME -RT Patch.

Updated Wireward To Last Revision.

Fixes - To The Scheduler MuQSS To Make Games Happier.

Kernel Now Have ZfsOnLinux By Default Can Be Compiled As Module Or Built-IN.

Union Aufs Updated.

* Disclaimer. =

This Kernel Patches On Top The Linux Official Kernel Vanilla From Kernel.org Comes With Absolutely
No Warranty . You Are On Your Own If A Device Get Bricked Well Just Say Bricked In The Name Of Science.
Just Dont Blame JavaShin .......  

You Have Been Warned.
Here There Will Be Dragons.
 


* This Linux Kernel Have Some Additions That Are Not In The Main Tree.
  Some Of Them Are Optimizations And New Features Like : >

1. CONFIG_PREEMPT_RT Patches > https://rt.wiki.kernel.org/index.php/Main_Page .
   
   * Selecting Expert Mode In Kernel Config To Make The Linux Kernel Full Realtime

2. ZEN-SOURCES -ZEN Patches > https://github.com/zen-kernel/zen-kernel .
   
   * ZEN-INTERACTIVE
   
   * mm-Proactive-compaction
   
   * ZEN-Add-sysctl-and-CONFIG-to-disallow-unprivileged-C 
   
3. Con Kolivas -CK Patches > http://ck-hack.blogspot.com .
   
   * MuQSS version 0.196 for linux-5.4 Multiple Queue Skiplist Scheduler As An Optional Choice

4. Distro Specific Patches ArchLinux + Gentoo/Linux + Debian/Ubuntu + Intel Clear/Linux .

5. Added Script To Debloat The Linux Kernel And Free It Of Privative Firmware And Convert It Into -libre -gnu Linux .

6. Some Optimizations And Fixes Added .
  
   * LL-kconfig-add-750Hz-timer-interrupt-kernel-config Thanks To Piotr Górski 
  
   * zswap-b-tree.patch
  
   * turbosched-v4.patch
  
   * ZFS-fix.patch
  
   * -O3 patch To Compile With The Level 3 Of Compilers Optimizations
  
   * graysky's GCC patch To Be Able To Select -march=native
  
   * ksm-patches.patch userspace-assisted KSM Thanks To  Oleksandr Natalenko 

7. Wireward Patches Updates For 5.4 Kernel . 
   
   https://www.wireguard.com

8. UnionFS AUFS .
  
   http://aufs.sourceforge.net/

9. Reiser4 - ReiserFS4 .

   https://sourceforge.net/projects/reiser4/

10. Conflict Fixing ETC .
    Carlos Jimenez (JavaShin-X) 2020
    Contact Me On My Gitter Unix-Like-Latino Community 
    https://gitter.im/Chat-Unix-Like/community


* COPYING. =

The Linux Kernel is provided under:

	SPDX-License-Identifier: GPL-2.0 WITH Linux-syscall-note

Being under the terms of the GNU General Public License version 2 only,
according with:

	LICENSES/preferred/GPL-2.0

With an explicit syscall exception, as stated at:

	LICENSES/exceptions/Linux-syscall-note

In addition, other licenses may also apply. Please see:

	Documentation/process/license-rules.rst

for more details.

### For Gentoo/Linux Only ZFS Inject Plus Clang Compile . ### 
See < > Clang-Compiling.md

### For Ubuntu/Debian Compilation And ZFS Injection Compilation With GCC . ###
See < > UPGRADED-COMMANDS-FOR-REALTIME-X-ON-UBUNTU-DEBIAN.md







