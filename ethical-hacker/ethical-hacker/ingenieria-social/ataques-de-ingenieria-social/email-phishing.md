---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Email Phishing

With _**phishing**_, an attacker presents to a user a link or an attachment that looks like a valid, trusted resource. When the user clicks it, he or she is prompted to disclose confidential information such as his or her username and password. Example 4-1 shows an example of a phishing email.

_**Example 4-1**_ _**-**_ _Phishing Email Example_

```
Subject: PAYMENT CONFIRMATION
Message Body:
Dear sir,We have discovered that there are occasional delays from our accounts department in making complete payments to our suppliers.This has caused undue reduction in our stocks and in our production department of which suppliers do not deliver materials on time.The purpose of this letter is to confirm whether or not payment has been made for the attached supplies received.Kindly confirm receipt and advise.
Attachment: SD_085_085_pdf.xz / SD_085_085_pdf.exeMD5 Checksum of the attachment: 0x8CB6D923E48B51A1CB3B080A0D43589D
```

**Spear Phishing**

_**Spear phishing**_ is a phishing attempt that is constructed in a very specific way and directly targeted to specific groups of individuals or companies. The attacker studies a victim and the victim’s organization in order to be able to make emails look legitimate and perhaps make them appear to come from trusted users within the company. Example 4-2 shows an example of a spear phishing email.

In the email shown in Example 4-2, the threat actor has become aware that Chris and Omar are collaborating on a book. The threat actor impersonates Chris and sends an email asking Omar to review a document (a chapter of the book). The attachment actually contains malware that is installed on Omar’s system.

_**Example 4-2**_ _-_ _Spear Phishing Email Example_

```
From: Chris ClevelandTo: Omar SantosSubject: Please review chapter 3 for me and provide feedback by 2pm
Message Body:Dear Omar,
Please review the attached document.
Regards,Chris
Attachment: chapter.zipMD5 Checksum of the attachment: 0x61D60EA55AC14444291AA1F911F3B1BE
```

**Whaling**

_**Whaling**_, which is similar to phishing and spear phishing, is an attack targeted at high-profile business executives and key individuals in a company. Like threat actors conducting spear phishing attacks, threat actors conducting whaling attacks also create emails and web pages to serve malware or collect sensitive information; however, the whaling attackers’ emails and pages have a more official or serious look and feel. Whaling emails are designed to look like critical business emails or emails from someone who has legitimate authority, either within or outside the company. In whaling attacks, web pages are designed to specifically address high-profile victims. In a regular phishing attack, the email might be a faked warning from a bank or service provider. In a whaling attack, the email or web page would be created with a more serious executive-level form. The content is created to target an upper manager such as the CEO or an individual who might have credentials for valuable accounts within the organization.

The main goal in whaling attacks is to steal sensitive information or compromise the victim’s system and then target other key high-profile victims.
