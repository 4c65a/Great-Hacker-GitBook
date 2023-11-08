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

# Ingeniería social

Influence, interrogation, and impersonation are key components of social engineering. Elicitation is the act of gaining knowledge or information from people. In most cases, an attacker gets information from a victim without directly asking for that particular information.

How an attacker interrogates and interacts with a victim is crucial for the success of a social engineering campaign. An interrogator can ask good open-ended questions to learn about an individual’s viewpoints, values, and goals. The interrogator can then use any information the target revealed to continue to gather additional information or to obtain information from another victim.

It is also possible for an interrogator to use closed-ended questions to get more control of the conversation and to lead the conversation or to actually stop the conversation. Asking too many questions can cause the victim to shut down the interaction, and asking too few questions may seem awkward. Successful social engineering interrogators use a narrowing approach in their questioning to gain as much information as possible from the victim.

Interrogators pay close attention to the following:

The victim’s posture or body language The color of the victim’s skin, such as the face color becoming pale or red The direction of the victim’s head and eyes Movement of the victim’s hands and feet The victim’s mouth and lip expressions The pitch and rate of the victim’s voice, as well as changes in the voice The victim’s words, including their length, the number of syllables, dysfunctions, and pauses With pretexting, or impersonation, an attacker presents as someone else in order to gain access to information. In some cases, it can be very simple, such as quickly pretending to be someone else within an organization; in other cases, it can involve creating a whole new identity and then using that identity to manipulate the receipt of information. Social engineers may use pretexting to impersonate individuals in certain jobs and roles even if they do not have experience in those jobs or roles.

For example, a social engineer may impersonate a delivery person from Amazon, UPS, or FedEx or even a bicycle messenger or courier with an important message for someone in the organization. As another example, someone might impersonate an IT support worker and provide unsolicited help to a user. Impersonating IT staff can be very effective because if you ask someone if he or she has a technical problem, it is quite likely that the victim will think about it and say something like, “Yes, as a matter of fact, yesterday this weird thing happened to my computer.” Impersonating IT staff can give an attacker physical access to systems in an organization. An attacker who has physical access can use a USB stick containing custom scripts to compromise a computer in seconds. Pharming is a type of impersonation attack in which a threat actor redirects a victim from a valid website or resource to a malicious one that could be made to appear as the valid site to the user. From there, an attempt is made to extract confidential information from the user or to install malware in the victim’s system. Pharming can be done by altering the host file on a victim’s system, through DNS poisoning, or by exploiting a vulnerability in a DNS server. Figure 4-1 illustrates how pharming works.

Figure 4-1 - Pharming Example

1 2 3 Legitimate website Malicious website

(looks legitimate)

Downloads malware User: Omar

(victim)

The following steps are illustrated in Figure 4-1:

Step 1 . The user (Omar) visits a legitimate website and clicks on a legitimate link.

Step 2. Omar’s system is compromised, the host file is modified, and Omar is redirected to a malicious site that appears to be legitimate. (This could also be accomplished by compromising a DNS server or spoofing a DNS reply.)

Step 3 . Malware is downloaded and installed on Omar’s system.

An attack that is similar to pharming is called malvertising. Malvertising involves incorporating malicious ads on trusted websites. Users who click these ads are inadvertently redirected to sites hosting malware.

TIP To help prevent pharming attacks, it is important to keep software up to date and run regular anti-malware checks. You should also change the default passwords in network infrastructure devices (including your home router). Of course, you also need to be aware of what websites you visit and be careful about opening emails.
