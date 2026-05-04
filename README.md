# Security-Operations-Center-Playbook-
# Incident Response Playbook
**Document Type:** Security Operations Center Playbook  
**Incident Type:** Ransomware Attack  
**Author:** Iseoluwa Ogunnaike  
**Date:** 4th May, 2026 
**Organisation:** SecureNow Ltd (Fictional)

---

## About Incident Response

Incident response is the structured process a company follows to detect, respond to, and resolve a cyberattack or security incident as quickly as possible. It acts as a clear guide that explains what actions should be taken immediately an incident occurs, helping teams manage the situation in an organised and effective way. Organisations need a formal playbook so that there is no confusion or delay during an attack, especially in the first critical moments where quick decisions can reduce damage. A company with a playbook can quickly identify the threat, contain it, and recover systems, while a company without one is more likely to panic, waste time on trial and error, and allow the attack to spread further. In the first 60 seconds of a serious attack, having no plan can lead to confusion and delayed action, which significantly increases the overall impact of the incident.


## About This Incident Type

Ransomware is a type of malicious software that encrypts files or systems, preventing users from accessing their data until a ransom is paid, usually in cryptocurrency. It typically enters an organisation through phishing emails, malicious links or attachments, compromised credentials, or unpatched software vulnerabilities. For a company like SecureNow Ltd, ransomware is especially dangerous because it stores sensitive financial data for 40,000 customers, making it a high-value target. If attackers gain access, they could encrypt critical systems and potentially expose personal data, leading to operational disruption, regulatory penalties under UK GDPR, and severe reputational damage.


## SecureNow Ltd - Company Profile

Read this carefully before you begin. Your playbook must be tailored to this company's specific environment. A generic playbook copied from the internet will not work here because it will not account for their actual systems, structure, and weaknesses.

**Company:** SecureNow Ltd  
**Size:** 52 employees, fully remote  
**Sector:** Financial technology (fintech), UK based  
**Infrastructure:** Google Workspace, AWS (hosts customer financial data), Slack, a third party payroll system, a CRM tool  
**Devices:** Mix of company issued laptops and personal devices. No MDM (Mobile Device Management) software is in place, meaning the company cannot remotely wipe or lock devices  
**Security team:** None. The Office Manager handles IT requests. There is no SOC, no SIEM, no dedicated security monitoring  
**Backups:** AWS data is backed up daily. Google Workspace data is not backed up separately outside of Google's own retention. The payroll system vendor manages its own backups but SecureNow has never tested a restore  
**MFA:** Enabled on Google Workspace but optional, 60 percent adoption. No MFA on AWS, CRM, or payroll system  
**Incident history:** A phishing email last year led to one employee clicking a malicious link. No malware was found but the company is not certain because no forensic investigation was done. The employee was asked to change their password  
**Communication:** The company uses Slack for almost all internal communication. There is no alternative communication channel if Slack is compromised  
**Current situation:** It is 7:30am on a Tuesday. The Office Manager has just arrived at her desk and received a message from three employees saying their laptops are showing a red screen with a message demanding payment in Bitcoin to unlock their files. A fourth employee's laptop appears to be unaffected. The Office Manager calls you, the SOC analyst  

---

## Your Playbook

Build each phase of the response below. Be specific to SecureNow Ltd. For every action you list, explain who does it, how, and why. Do not write generic steps. Write steps that could actually be followed by someone at this company right now.

---

### Phase 1: Detect and Triage

**Objective:** Confirm the incident is real, understand the initial scope, and establish who is responding.

**Guiding questions before you write your steps:**
- How do you confirm this is ransomware and not a hoax or a software glitch?
- Three laptops are affected. How do you find out if more are affected without triggering further spread?
- The company has no SIEM or security monitoring. What can you actually use to gather information right now?
- Who needs to be notified in the first 15 minutes? Remember, there is no security team

**Your steps for Phase 1:**

| Step | Action | Who | How | Why |
|------|--------|-----|-----|-----|
| 1.1 |Confirm this is a real ransomware incident |SOC Analyst (me) | I will ask affected users to send a clear photo of the red screen using a non infected device. I will look out for the messages and cryptocurrecy payment instructions and cross-check that multiple users are seeing similar messages. |This helps to confirm the incident is real |
| 1.2 |Identify initial scope of affected systems |SOC Analyst and the Office Manager|Contact all staffs via Slack to ask of they have the same red screen or they are able to access files|This allows rapid scoping without triggering further execution of malware. |
| 1.3 |Gather available logs and evidence from existing platforms |SOC Analyst (me)|I will access Google Workspace Admin logs to check for suspicious logins or file activity. Review AWS CloudTrail for unusual API activity or access patterns. Ask affected users what they did before the issue appeared, such as opening emails or downloading files. |Since there is no SIEM or endpoint detection, these are the only available sources of visibility to begin understanding timeline and potential entry point. |
| 1.4 |Establish incident response leadership and notify key stakeholders |Office Manager |Immediately notify the CEO and assign temporary incident lead responsibility to the Office Manager with your guidance. |With no security team in place, clear leadership and escalation in the first 15 minutes is critical to avoid confusion, delays, and poor decision making during a fast-moving incident. |


**Your reasoning:** Write 2 to 3 sentences explaining your overall approach in this phase and any judgment calls you made.

> In my approach I prioritised quickly confirming the incident and assessing its scope using only available resources such as user reports, Google Workspace logs, and AWS activity, since no security monitoring tools are in place. I made the judgment to limit interaction with affected devices to avoid triggering further spread or destroying evidence, while still gathering enough information to act. 


---

### Phase 2: Contain

**Objective:** Stop the ransomware from spreading to more systems and data.

**Guiding questions before you write your steps:**
- The company uses personal devices. You cannot remotely wipe them. What can you do instead?
- Ransomware often spreads through shared network drives. Does SecureNow Ltd have shared drives in Google Workspace or AWS that could be at risk?
- Should you disconnect the affected laptops from the internet immediately? What is the risk of doing that too quickly versus too slowly?
- Slack is potentially compromised or could be used by the attacker to monitor communications. What do you do about this?

**Your steps for Phase 2:**

| Step | Action | Who | How | Why |
|------|--------|-----|-----|-----|
| 2.1 |Isolate affected devices immediately |Affected employees guided by SOC Analyst |Instruct affected users via phone call to turn off WiFi and disconnect from any networks immediately. |This stops the ransomware from spreading to other systems or shared resources |
| 2.2 |Stop use of shared drives and cloud access temporarily |SOC Analyst with Office Manager |In Google Workspace, temporarily restrict access to shared drives and file sharing. In AWS, review and limit access permissions where possible. |Ransomware can spread through shared storage, so limiting access reduces the risk of further encryption or data compromise. |
| 2.3 |Move communication off Slack |Office Manager |Instruct all staff via Slack to stop discussing the incident there and switch to an alternative such as personal email or phone calls. |Slack could be monitored if compromised|
| 2.4 |Identify and isolate any additional affected devices |SOC Analyst with all employees |contact any suspected users and instruct them to disconnect from the internet immediately if they notice unusual behaviour. |Early containment reduces the number of infected systems |
| 2.5 |Temporarily disable high-risk accounts and access points |SOC Analyst |Disable or reset credentials for accounts showing suspicious activity, especially in Google Workspace and AWS. |If ransomware entered through compromised credentials, this prevents further attacker access and lateral movement. |

**Your reasoning:** Write 2 to 3 sentences explaining your overall approach in this phase and any judgment calls you made.

> My approach focused on rapidly isolating affected systems and limiting access to shared resources to prevent further spread, while working within the constraint of having no remote management tools. I made the judgment to disconnect devices from the network but not power them off immediately, to preserve potential evidence for investigation. I also decided to move communication away from Slack early, given the risk that it could be monitored or compromised during the incident.


---

### Phase 3: Eradicate

**Objective:** Remove the ransomware from affected systems and identify how it got in.

**Guiding questions before you write your steps:**
- You need to find the root cause. Given the company's history with a phishing click last year and optional MFA, what are the most likely entry points?
- The affected laptops are a mix of company and personal devices. How does this complicate eradication?
- Should you pay the ransom? Think carefully before answering this. There are legal, ethical, and practical dimensions to consider

**Your steps for Phase 3:**

| Step | Action | Who | How | Why |
|------|--------|-----|-----|-----|
| 3.1 |Identify the likely entry point |SOC Analyst |Review Google Workspace login logs for unusual access, check AWS CloudTrail for suspicious activity, and interview affected users about recent emails, links, or downloads. Focus on phishing emails and credential compromise due to weak MFA. |Understanding how the ransomware entered is critical to prevent reinfection |
| 3.2 |Remove or rebuild infected devices |Affected employees with guidance from SOC Analyst |Instruct users to stop using infected devices. For company laptops, perform a full system wipe and reinstall the operating system. For personal devices, advise a full reset |Rebuilding ensures the malware is completely eliminated. |
| 3.3 |Secure all accounts and enforce stronger access controls| SOC Analyst with Office Manager|Reset passwords for all users, enforce MFA across Google Workspace, AWS, CRM, and payroll systems, and review account permissions for any suspicious changes. |If attackers gained access through credentials, this step removes their access and prevents further compromise. | |
| 3.4 |Scan and verify all systems before reconnecting |SOC Analyst |Before allowing devices back on the network, ensure they are rebuilt and checked using available antivirus tools or external support if needed. Only reconnect clean systems. |This prevents reinfection and ensures the environment is safe before normal operations resume. |

**Ransom decision:** Should SecureNow Ltd pay the ransom? Write 4 to 5 sentences arguing your position. Consider: legal guidance in the UK, whether payment guarantees recovery, and what paying signals to attackers.

> SecureNow Ltd should not pay the ransom. Guidance from the National Cyber Security Centre and National Crime Agency advises against payment because it does not guarantee that data will be restored or that attackers will not retain or resell the data. Paying may also create legal risk if the funds reach sanctioned individuals or groups under UK regulations. In addition, payment signals that the organisation is willing to comply, which can make it a target for future attacks. The safer and more sustainable approach is to focus on containment, eradication, and recovery from backups while engaging law enforcement and incident response specialists.


---

### Phase 4: Recover

**Objective:** Restore systems and data and return the business to normal operations safely.

**Guiding questions before you write your steps:**
- AWS data is backed up daily. The payroll backups have never been tested. What does that mean for your recovery plan?
- How do you verify that restored systems are clean before connecting them back to the network?
- The business cannot operate if staff cannot access Google Workspace. What is the priority order for recovery?
- 40,000 customers have their financial data on this system. At what point do you tell them something happened?

**Your steps for Phase 4:**

| Step | Action | Who | How | Why |
|------|--------|-----|-----|-----|
| 4.1 |Verify integrity of backups before restoring |SOC Analyst with AWS support | Check AWS backups for signs of encryption or unusual changes. Restore a small sample in an isolated environment to confirm data is usable. Contact payroll vendor to confirm backup status and request a test restore.|Ensures backups are clean and usable before relying on them, especially since payroll backups have never been tested |
| 4.2 |Rebuild and prepare clean systems for use |SOC Analyst with employees |Ensure all infected devices have been wiped and reinstalled. Apply basic security controls such as updated antivirus and enforced MFA before reconnecting to systems. |Prevents reinfection and ensures only clean, secured devices return to the environment. |
| 4.3 |Restore access to critical systems in priority order |SOC Analyst with Office Manager |First restore access to Google Workspace for communication and operations. Then restore AWS systems hosting customer data. Finally, confirm CRM and payroll system access. |Google Workspace is critical for daily operations, followed by customer data systems, ensuring business continuity is restored in a controlled way. |
| 4.4 |Validate systems are clean before full reconnection |SOC Analyst |Monitor for unusual activity in Google Workspace and AWS after restoration. Check login activity, file changes, and permissions for anomalies before allowing full usage. |Confirms that no attacker access or malware remains before normal operations resume. |
| 4.5 |Notify stakeholders and customers if required |CEO with legal guidance |Assess whether personal data was accessed or at risk. If so, report the breach to the ICO within 72 hours and inform affected customers with clear communication. |Ensures compliance with UK GDPR and maintains transparency, reducing legal and reputational risk. |

**Your reasoning:** Write 2 to 3 sentences explaining your recovery priority decisions.

My recovery priority focused on restoring Google Workspace and Slack first because it is essential for communication and coordinating all further recovery actions. AWS systems hosting customer financial data were restored next to ensure business continuity, but only after verifying backups were clean. Lower priority systems such as payroll and CRM were restored afterwards, especially given the uncertainty around untested payroll backups, to reduce the risk of reintroducing issues.


---

### Phase 5: Lessons Learned

**Objective:** Understand what happened, why it happened, and how to prevent it happening again.

This is not optional. A company that does not conduct a lessons learned review after an incident is almost certain to have the same incident again.

**Complete the following:**

**Root cause identified:**
What do you believe the most likely entry point was, and what specific weakness made it possible?

> The most likely entry point was a phishing email that tricked an employee into clicking a malicious link or entering their login credentials. This was made possible by weak security controls, particularly the lack of enforced multi factor authentication on key systems like AWS, CRM, and payroll, as well as limited user awareness from the previous phishing incident.


**What went well (if anything):**
Were there any controls or actions that helped limit the damage? Be honest. If nothing went well, say that and explain why.

> Some controls did help limit the damage, although they were limited. The AWS environment had daily backups in place, which increases the likelihood that critical customer financial data can be restored without paying the ransom. The incident was also identified early through employee reports, which allowed a faster response before it spread further across all devices.

**What failed:**
List at least four specific security gaps this incident revealed about SecureNow Ltd.


* Lack of enforced multi factor authentication across key systems 
* No endpoint management or MDM
* Absence of security monitoring tools such as SIEM or EDR
* No VPN or secure access control for remote workers.
* Overreliance on Slack as the only communication channel.
* Untested backup processes for the payroll system
* Lack of a formal incident response plan or dedicated security team.


**Recommendations:**
For each gap you identified, write one concrete recommendation. Be specific. "Improve security" is not a recommendation. "Enforce MFA on all systems including AWS, CRM, and payroll within 30 days" is a recommendation.

* Enforce multi factor authentication across all systems including AWS, CRM, and payroll within 30 days, using app based authenticators and making it mandatory for all users
* Implement a Mobile Device Management solution within 60 days to enable device monitoring, remote wipe, and enforcement of security policies on both company and personal devices
* Deploy a basic security monitoring solution such as a cloud based SIEM or managed detection and response service within 90 days to provide visibility into logs and suspicious activity
* Introduce a VPN or zero trust network access solution for all remote employees within 60 days to secure connections to company systems and reduce exposure to external threats
* Establish an alternative secure communication channel such as Microsoft Teams or emergency email distribution lists within 30 days to be used during incidents if Slack is compromised
* Conduct a full backup and restore test for the payroll system within 30 days and schedule quarterly testing to ensure reliability
* Develop and implement a formal incident response plan within 45 days, including defined roles, escalation paths, and regular tabletop exercises for staff training


**Regulatory considerations:**
Under UK GDPR, organisations must report a personal data breach to the ICO within 72 hours of becoming aware of it. Based on what you know about SecureNow Ltd and this incident, does this reporting obligation apply? What happens if they miss the deadline?

> Yes, the reporting obligation is likely to apply. SecureNow Ltd handles financial data for 40,000 customers, and a ransomware attack creates a high risk that personal data has been accessed, encrypted, or exfiltrated, even if this is not yet fully confirmed. Under UK GDPR, the company should report the incident to the Information Commissioner's Office within 72 hours of becoming aware of it, especially given the potential impact on individuals.

If they miss the deadline, they must still report the breach and provide a valid reason for the delay. Failure to report on time without justification can lead to regulatory investigation, enforcement action, and significant fines, as well as increased reputational damage.

---

## Critical Thinking Questions

Answer each question in 3 to 5 sentences.

**Question 1:** The company uses Slack as its only internal communication channel. During a ransomware incident, attackers sometimes monitor internal communications to understand the response and adapt. What should SecureNow Ltd do about this and why does it matter?

> SecureNow Ltd should assume Slack may be compromised and immediately stop using it for sensitive incident discussions. The Office Manager should instruct staff to switch to alternative channels such as phone calls or personal email, and limit Slack use to brief operational notices only. This reduces the risk of attackers monitoring conversationns.

**Question 2:** The Office Manager is the only person handling IT at this company. During a major incident at 7:30am, she is now being asked to make decisions that would normally require a CISO, legal team, and incident response firm. What does this tell you about the company's security posture and what would you recommend they put in place before the next incident?

> This indicates that SecureNow Ltd has a weak and immature security governance and no structured incident response capability. Relying on a single Office Manager for critical decisions during a ransomware attack creates delays, increases the risk of poor judgment, and exposes the company to legal and operational mistakes.

The company should establish a basic security structure before the next incident. This should include assigning a dedicated security lead or virtual CISO, creating a formal incident response plan with clearly defined roles, and pre engaging an external incident response firm and legal counsel. Regular training and tabletop exercises should also be introduced so staff understand their responsibilities and can respond effectively under pressure.


**Question 3:** A journalist contacts SecureNow Ltd asking if they have been hit by ransomware. They heard from a source. The CEO asks you what to say. What do you advise and why?

> I would advise the CEO not to confirm or deny the incident at this stage, but to provide a controlled holding statement. For example, they can say the company is aware of a potential security issue, is currently investigating, and will provide updates once more information is confirmed. All external communication should be coordinated with legal counsel to ensure compliance with UK GDPR and to avoid making inaccurate or premature statements.

---

*Template provided by CyberShift With Funke | Cohort 1 Assignment*
