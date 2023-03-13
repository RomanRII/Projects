## Proxyshell2RCE
### What is Proxyshell2RCE
* https://github.com/RomanRII/proxyshell2rce
* This was developed using a non-weaponized POC of proxyshell located here: https://github.com/dmaasland/proxyshell-poc
* This was developed prior to any weaponized versions being released. I utilized https://y4y.space/2021/08/12/my-steps-of-reproducing-proxyshell/ to understand the POCs functionality and what context we are launched in when exploitation is successful.

## What it does
* The tool starts by sending a valid user an email with an encoded (Using encoder.cpp) ASPX file as the attachment.
* Once the email is sent to the user and ends up in the mailbox, we utilize `New-ManagementRoleAssignment` to assign the `Mailbox Import Export` rights to the targeted user.
* During exploitation, it was noted that mail export requests can get stuck and fail to terminate. So running `Get-MailboxExportRequest | Remove-MailboxExportRequest -Confirm:$false` was required during the execution.
* We then leverage `New-MailboxExportRequest` to export the email from the target user's mailbox. We filter emails by searching for our supplied email Subject. Once found, we save the export to `\\\\127.0.0.1\\C$\\inetpub\\wwwroot\\aspnet_client\\*.aspx`
* Because we encoded our ASPX file prior to sending the email, the ASPX is then double encoded by the export request. Which allows the ASPX file to be properly executed when accessed via the browser.
* In my POC, I utilized an ASPX which downloaded a second stage webshell and dropped onto disk. 
![image](https://pbs.twimg.com/media/E80HEFkVIAggG1R?format=jpg&name=large)
