# boot-grub
How do I boot my PC from GRUB? [duplicate] Asked 3 years, 4 months ago Active 2 years, 5 months ago Viewed 107k times  16   12 This question already has answers here: How can I repair grub? (How to get Ubuntu back after installing Windows?) (14 answers) Closed 2 years ago. I can no longer boot Ubuntu following a corruption problem initially reported here (How do I solve the "invalid arch dependent elf magic" error message).  When I power my laptop, I now get the following message:  GNU GRUB version 2.02~beta2-9ubuntu1.7 Minimal BASH-like line editing is supported. For the first word, TAB lists possible command completions. Anywhere else TAB lists possible device or file completions." and then the prompt  grub> Can anyone help me get back to Ubuntu ?  boot grub2 share  improve this question  follow  edited Jul 2 '17 at 18:17  You'reAGitForNotUsingGit 13.4k99 gold badges3838 silver badges7373 bronze badges asked Jun 28 '17 at 7:49  Mons 15911 gold badge33 silver badges77 bronze badges Comments are not for extended discussion; this conversation has been moved to chat. – Thomas Ward♦ Jul 2 '17 at 19:03 Big thumbs up to everybody. I chased down a few leads and finally solved the problem by booting from a live CD and entering the command "sudo update-grub" @derHugo your help was massively useful. – Mons Jul 2 '17 at 19:29 1 The various hints given by @derHugo can be found on the chat site on Stack Exchange here: chat.stackexchange.com/rooms/61451/… and in particular when he recommended googling the question, here: "Haha sorry always forget that ^^ anyway please Google it there are tons of articles addressing this issue e.g. here is another one". Anyway, I'm absolutely made up to be up and running on my laptop again. I know I'm not supposed to say thanks, but I will all the same. THANKS ! – Mons Jul 2 '17 at 21:59 add a comment 3 Answers  35  Ok, from grub type ls (hd0,1)/ you should see a file named vmlinuz or linux, and initrd.img  Type linux (hd0,1)/vmlinuz root=/dev/sda1 or linux (hd0,1)/linux root=/dev/sda1 depending on what you found with ls (hd0,1)/, then:  initrd (hd0,1)/initrd.img boot If you get initramfs rescue mode enter your password, then startx. You should now have a desktop.  Use gparted to check your file system, if it reports an error, then you need to boot from a LiveCD or other media to fix it .... DO NOT attempt to repair a mounted partition.  The following three commands fix many grub boot problems. They run quick so just do all three instead of trying to find which one you need.  sudo grub-install /dev/sda &amp;&amp; sudo update-grub &amp;&amp; sudo update-initramfs -u Reboot and see what you get.  share  improve this answer  follow  edited Feb 2 '18 at 5:55 answered Jul 2 '17 at 18:49  ravery 6,11955 gold badges1616 silver badges3535 bronze badges 3 Is it really innitrd or should it be initrd? – WinEunuuchs2Unix Jul 2 '17 at 19:52 1 It is actually initrd – answerSeeker Jul 2 '17 at 20:19  1 @ravery Yes I could have corrected the typo. I have a weird point of view thinking it's more polite to point out to the author and letting them make the change. That way an otherwise spotless answer doesn't have the "blemish" of an "edited by someone else" flag. I do edit new users' questions frequently though... Have another +1 :) – WinEunuuchs2Unix Jul 2 '17 at 22:18  1 IF you stuck in "INITRAMFS" not in a fully booted system you can't use startx cause there is no desktop there, what you are referring as initramfs should be multi-user.target. – Ravexina♦ Jul 5 '17 at 8:53  3 In case the files above aren't listed, try iterating on ls (hd0,1)/ command, as in: ls (hd0,2)/, ls (hd0,3)/, etc. as suggested in here. – Nae Dec 23 '18 at 17:46  show 9 more comments  1  The most probable cause to that issue is installing the OS to a disk, grub to a different disk that is not removable. Then removing the OS disk.  You could just plug the USB stick back in. Problem solved.  share  improve this answer  follow  edited Jul 2 '17 at 19:17 answered Jul 2 '17 at 19:02  RobotHumans 26.2k33 gold badges6969 silver badges109109 bronze badges Solution found (see above). – Mons Jul 2 '17 at 19:29 I saw the chat conversation. Solved with update-grub, which supports not refutes this answer. – RobotHumans Jul 2 '17 at 19:32 add a comment  1  Restart your system. Press f2 key while loading. Goto boot option. Press f5/f6 to change values (which os you want to install keep it in first place.). Enter f10 key....It may solve your problem. . . . If not enter this in grub rescue mode.... ls (hd0) (hd0,msdos6) (hd0,msdos5)....(hd0,msdos1) OR (hd0) (hd0,gpt6).....(hd0,gpt1)  set boot=(hd0,gpt6) OR set boot=(hd0,msdos6) set prefix=(hd0,gpt6)/boot/grub OR use msdos6 instead. insmod normal normal This may solve your problem.  share  improve this answer  follow  answered Jul 9 '17 at 8:11  Pavan Rao 1122 bronze badges these are various ways to launch grub. this is not the issue as OP states. grub launches but drops to recovery mode. The issue is that the grub config file is missing – ravery Jul 9 '17 at 8:23 add a comment Not the answer you're looking for? Browse other questions tagged boot grub2 or ask your own question.
