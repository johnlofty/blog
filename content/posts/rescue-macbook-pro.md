---
title: "Rescue My Macbook Pro 💻"
date: 2023-03-18T11:52:57+08:00
draft: false
---

## Background 

I accidentally spilled a WHOLE GLASS of WATER on my MacBookPro about two month ago. Even though I immediately shut it down, and left it on the table to dry out for about 3 days. I'm pretty sure there was still a lot of water inside. So I had to take it to a private repair shop to fix it. 

## Why didn't I take it to the Apple Store?

Because it cost me a fortune to let Apple repair it. A local Apple authorized repair shop told me the total cost is as high as 8000 CNY (about 1161$), as they would need to replace the entire motherboard and keyboard. Apparently this price is not even worth it.

At last the private repair shop took me 1300 CNY(188$) and nearly one month to fix it but not the touchID module. And they update my Mac from Monterey(12) to Ventura(13) to troubleshoot software issues.

You know the giant leap between macOS 12 and macOS 13, especially the System Preference, which is totally different. I can't get used to it. I often found myself lost in System Preference menus, most of the time I need to Google where the settings are.

## The anonying bug on macOS Ventura - "Login items added"

Here's an image of "Login items added" bug. 

![login-item-bug](rescue_mac/login-item.jpeg)

Usually this notification shows at the first time you install an app, or when you login.

But in my case, **EVERY TIME** I click into the **Login items** in System settings,  macOS pops up new "Login items added" notification in a row. yeah **EVERY TIME**! Good Job Apple!

![login-item-added](rescue_mac/login-item-2.jpg)
[check this on twitter](https://twitter.com/luciascarlet/status/1590017535910760450)

You can read more about this bug.
* [https://www.macrumors.com/2023/02/02/macos-background-items-added-notification-bug](https://www.macrumors.com/2023/02/02/macos-background-items-added-notification-bug/)
* [https://iboysoft.com/news/where-are-login-items-macos-ventura.html](https://iboysoft.com/news/where-are-login-items-macos-ventura.html)

This bug tortures me everyday. Even after I upgrade macOS to latest 13.2.1, it's still there.

Finally, at one late night I decided to downgrade to Monterey.

## Downgrade from Ventura to Monterey

I checked several methods to downgrade macOS. I decided to make a bootable installer.

I followed the instructions.
* erase my USB drive ✅
* download Monterey from App Store ✅
* make it bootable using commands ✅
* restart Mac while holding option key ✅
* erase internal drive ✅
* boot from USB ❌

When I chose boot from USB drive, my Mac says it need to download something from the Internet. I gave it my WIFI password, then after download for about 10 minutes, It showed some error code like `-2100f` or `-1008f`. No matter how many times I tried, It always fail.

After Google around for some minutes, I realize I made a mistake, I forgot to close *Find My* service, and I didn't logout my iCloud account. 
However, even I erased Mac from *Find My* on iPhone, Mac still refused to boot from USB. And because I already erase the internal drive, I can't boot from old system in Mac.

My Mac is bricked(🧱) and I'm stuck.


## Recover Mac using Apple Configurator

I tried to get advice from Apple Support, wondering if I need to bring it back to a repair store. A very kind and patient guy from Apple customer service advised me to recover my Mac from another Mac using Apple Configure. This gave me hope.

There is a detailed guide on Apple website, which tells you what to do in every steps.  

Apple's guide of [how to recover your mac using Apple Configurator](https://support.apple.com/zh-cn/guide/apple-configurator-mac/apdebea5be51/mac)

But I want complain that the steps Apple told you to get mac into DFU mode is not quite right. I tried many times, still failed to enter DFU mode.

you can follow these instructions to enter DFU mode.
* [how to enter DFU mode on intel mac](https://www.youtube.com/watch?v=UaVgBP4gJsU)

After fix the problem of entering into DFU mode, I found another challenge. **the two Mac's OS version must match!** otherwise the recover process will fail.

In my case, my Mac was macOS Ventura, so the other Mac has to be Ventura too. Good job Apple!

Finally, after upgrade the other Mac to Ventura, I successfully rescued my Mac. I downgrade macOS to 10.14(Mojave). I will stay on this version for a very long time.


## Take-away advices

![keep water out of your fking mac](rescue_mac/keep_out.jpg)
1. Keep your water out of your fking Mac, unless you have Apple Care.🤣
2. If you want to downgrade you Mac, remember to close *Find My* and logout your AppleID.
3. Apple really needs to control its software quality.😠



## ChatGPT improved version

so much better than the original version. AI rocks!🚀

--- 

A few months ago, I accidentally spilled a whole glass of water on my MacBookPro, Despite shutting it down imeediately and leaving it to dry for three days, I was pretty sure that there was still a lot of water inside. As as a result, I took it to a private repair shop instead of an Apple Store because I couldn't afford the hefty price tag of Apple's repair services. An Apple authorized repair shop quoted me a staggering 8000 CNY (about 1161 USD) to replace the entire motherboard and keyboard, which was not worth the investment.

The private repair shop fixed my MacBook for 1300 CNY (188USD), but they could not repair the touchID module. They upgraded my Mac from Monterey(12) to Ventura(13) to troubleshoot software issues. Unfortunately, the giant leap between macOS 12 and macOS 13, especially the System Preference, was challenging to get used to. I found myself lost in System Preference menus, and I had to search online for the settings.

The Annoying bug on macOS Ventura - "Login items added" - made my experience even worse. The notification usually appears the first time you install an app or log in. However, in my case, the notification popped up every time I clicked into the Login items in System settings. This bug frustrated me every day, even after upgrade to the latest version of macOS 13.2.1

One late night, I decided to downgrade to Monterey. I looked up several methods to downgrade macOS and decided to create a bootable installer. I followed the instructions, including erasing my USB drive, downloading Monterey from the App Store, and making it bootable using commands. However, when I tried to boot from the USB drive, my mac required me to download something from the Internet. After downloading for about ten minutes, I received an error code like -2100f and -1008f, and the process failed repeatedly.

After some research, I realized that I made a mistake by forgetting to close *Find My* service and not logging out of my iCloud account. Even after erasing my Mac from *Find My* on my iPhone, my Mac still refused to boot from USB. Additionally, because I had erased the internal drive, I couldn't boot from the old system on my Mac, and my device was bricked.

I sought advice from Apple Support, and they recommended recovering my Mac using another Mac through Apple Configurator. Although there was a detailed guide on Apple's website, I found that the steps to get my Mac into DFU mode were not quite right. After some trial and error, I discovered a way to enter DFU mode on Intel Macs. However, I faced another challenge because the two Macs' OS versions had to match, meaning that the other Mac also had to be running Ventura.

After upgrading the other Mac to Ventura, I successfully downgrade macOS to 10.14(Mojave), which I will stay on for a very long time.

In summary, keep water away from your Mac, unless you have Apple Care. If you want to downgrade your Mac, remember to close *Find My* and log out of your Apple ID. Apple must improve its software quality.