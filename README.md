# Current Projects
## ChaosC2
### What is ChaosC2
* ChaosC2 is a custom private C2 framework.
* ChaosC2 is built to replicate functions as seen within Cobalt Strike with more OPSEC in mind alongside custom implementations.
* ChaosC2 is for in-house utilization only. Commercial/Open-Source usage is not yet planned.
### Technical Specifications
* ChaosC2's TeamServer is built using Python 3.10.10
* ChaosC2's Windows Client is built using C# .NET Framework 4.8
* ChaosC2's Beacon is built using C++

![image](https://user-images.githubusercontent.com/74742067/224641246-ce5dbde3-991e-438d-82de-689c3fd62c13.png)

# Previous Projects
## Jenkins-Strike
### What is Jenkins-Strike
* Jenkins-Strike is a portable Jenkins build configuration which aims to aid Red Teamers in Cobalt Strike profile generation.
* Inspiration to build an automated Cobalt Strike profile generator came from https://github.com/threatexpress/random_c2_profile
* Private version is consistently updated adding techniques/items discovered from research
* Jenkins-Strike utilizes a Python3 tool to generate/modify the profile based off of the Jenkins buiild parameters. 

![image](https://user-images.githubusercontent.com/74742067/210201496-db3f69a2-f21b-4d89-91c7-d17f764f76f5.png)

## CrackMapExec FTP Protocol Addition
### What is this
* I implemented FTP protocol functionality into a branch CrackMapExec and submitted a pull request which was then approved and merged.
* https://github.com/Porchetta-Industries/CrackMapExec/pull/639
* https://github.com/Porchetta-Industries/CrackMapExec/commit/21b5adb138779b99702321dacfc7de12524d9643
* Future improvements and contributions are planned

## Proxyshell2RCE
### What is Proxyshell2RCE
* https://github.com/RomanRII/proxyshell2rce
* This was developed using a non-weaponized POC of proxyshell located here: https://github.com/dmaasland/proxyshell-poc
* This was developed prior to any weaponized versions being released. I utilized https://y4y.space/2021/08/12/my-steps-of-reproducing-proxyshell/ to understand the POCs functionality and what context we are launched in when exploitation is successful.
* The tool works by sending a valid user an email with a encoded (Using encoder.cpp) ASPX file.
  *  Once the email is sent to the user and ends up in the mailbox, we utilize `New-ManagementRoleAssignment` to assign the `Mailbox Import Export` rights to the targeted user.
  * During exploitation, it was noted that mail export requests can get stuck and fail to terminate. So running `Get-MailboxExportRequest | Remove-MailboxExportRequest -Confirm:$false` was required during the execution.
  * We then leverage `New-MailboxExportRequest` to export the email from the target user's mailbox. We filter emails by searching for our supplied email Subject. Once found, we save the export to `\\\\127.0.0.1\\C$\\inetpub\\wwwroot\\aspnet_client\\*.aspx`
  * Because we encoded our ASPX file prior to sending the email, the ASPX is then double encoded by the export request. Which allows the ASPX file to be properly executed when accessed via the browser.
  * In my POC, I utilized an ASPX which downloaded a second stage webshell and dropped onto disk. 
![image](https://pbs.twimg.com/media/E80HEFkVIAggG1R?format=jpg&name=large)
