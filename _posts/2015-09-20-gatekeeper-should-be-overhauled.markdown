---
layout: post
title: "Gatekeeper should be overhauled"
date: 2015-09-20
categories:
---

Recently a major security incident, dubbed *XcodeGhost*, happened in China. In a nutshell, many developers in China, frustrated with the speed and instability when downloading Xcode from Mac App Store, resorted to third party sources. Some people deliberately poisoned these sources with a modified Xcode that inserts malware codes into any app it compiles. More than hundreds of iOS apps in China have been infected with this malware, including many from major corporations, like WeChat or Netease Music, and millions of devices have been affected.

Several parties are at fault here: *That which shall not be named*, responsible for the abysmal experience of network packets crossing China's borders; Mac App Store, which gets stuck in cryptic errors or restarts downloads whenever a network error is encountered; the developers and their organizations who should know better not to ignore system warnings, or know how to verify the digital signature by themselves.

But one thing is also responsible: Gatekeeper. Gatekeeper is a security feature in OS X, where if you open an app downloaded from the Internet for the first time, the launcher will do a check of its digital signature. If the signature is missing, or the contents of the application fail to match its signature, it will fail to launch. Had Gatekeeper properly functioned, the infected `Xcode.app` would have been detected.

So why did it not function? Most likely the users bypassed it or even disabled it altogether. We cannot protect those who do not wish to be protected. If disabled, Gatekeeper can do nothing at all. But why do they disable it in the first place? One reason may be that we send the wrong message.

# The warning dialog

![A warning dialog by Gatekeeper]({{ site.baseurl }}/images/gatekeeper_warning_google_chrome.png)

Let's first see what Gatekeeper presents to the user. Here is a dialog I get when opening a `Google Chrome.app` (downloaded with Google Chrome itself). It warns me that it is downloaded from the Internet. Huh? Don't I know that already? I downloaded it myself. I can't think of scenario where a user might be reminded that he/she downloads an app from the Internet and somehow forgets. **This dialog tells the user nothing new and nothing useful. It gets in the way and annoys users.** That is at least why I, when first exposed to the world of OS X, turned off Gatekeeper.

Moreover, the dialog shows a warning, but it is actually a sign of success. When this dialog pops up, the launcher has completed its verification of digital signature, and finds that app is pristine and trusted. If the verification fails, it shows an error dialog. If the app is not marked as downloaded from the Internet, or has been opened before, no digital signature check is performed. Of these three possibilities, the first one is actually the safest. Yet the UI gives a *negative* feedback to the user. **The Gatekeeper is like a naysayer who always complains, about even the perfectly good things. No wonder everyone wants to block him.**

To be actually useful, this dialog, after the verification succeeds, should be something like "This app is signed by [[Corporation or person name]]. Would you like to open it?". Or even better, just never pops up a dialog in case of success. Provide another way, preferably reachable from the context menu, to examine the chain of signers for the few who are interested.

# The error dialog

![An error dialog by Gatekeeper]({{ site.baseurl }}/images/gatekeeper_error_google_chrome.png)

When the application does not contain a digital signature, or the contents do not match the signature, an error dialog pops up. Except it does not look like an error. "Identity of the developer cannot be confirmed"? Do any person, not well versed in cryptography or software security, feel in any way threatened by this line?

Instead, it should have an icon signifies error, like ☠. The message should not be as soft. Instead, it should be close to *This app fails cryptographic check. It may be corrupted or infected with viruses.*. "Virus" is the word that will actually scares off ordinary users. Judging from the *XcodeGhost* incident, that message isn't far from truth at all.

-------------------------------------------------------------------------

In summary, Gatekeeper fails to keep the gates and therefore it should be improved. The UI it presents does not convey the true meaning accurately, and ordinary users are only annoyed, not protected by it.


