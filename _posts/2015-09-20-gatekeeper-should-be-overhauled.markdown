---
layout: post
title: "Gatekeeper should be overhauled"
date: 2015-09-20
categories:
---

Recently a major security incident, dubbed *XcodeGhost*, happened in China. In a nutshell, many developers in China, frustrated with the speed and instability when downloading Xcode from Mac App Store, resorted to third party sources. Some people deliberately poisoned these sources with a modified Xcode that inserts malware codes into any app it compiles. More than hundreds of iOS apps in China have been infected with this malware, including many from major corporations, like WeChat or Netease Music, and millions of devices have been affected.

Several parties are at fault here: *That which shall not be named*, responsible for the abysmal experience of network packets crossing China's borders; Mac App Store, which gets stuck in cryptic errors or restarts downloads whenever a network error is encountered; the developers and their organizations who should know better not to ignore system warnings, or know how to verify the digital signature by themselves.

But one thing is also responsible: Gatekeeper. Gatekeeper is a security feature in OS X, where if you open an app downloaded from the Internet for the first time, the launcher will do a check of its digital signature. If the signature is missing, or the contents of the application fail to match its signature, it will fail to launch. Had Gatekeeper properly functioned, the infected `Xcode.app` would have been detected.

So why did it not function? Most likely the users bypassed it or even disabled it altogether. We could certain blame the users here, and try to educate them not to ignore them in the future, citing *XcodeGhost* as an example. But more than that, we should improve the user experience of Gatekeeper.

