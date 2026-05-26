# Organizational OPSEC: Defending Against Infiltration, Informants, and Internal Threats

*Status: Level 2 Directive | Audience: Core Leadership and Security Teams*

The history of U.S. social movements is inseparable from the history of state infiltration. The FBI's COINTELPRO program systematically infiltrated, disrupted, and destroyed civil rights, anti-war, and Black liberation organizations through the 1950s–1970s. FBI files released through FOIA requests confirm that similar surveillance and infiltration programs have continued under different names — targeting environmental groups (THERMCON), animal rights organizations, Occupy Wall Street, and Black Lives Matter chapters in recent decades. Private corporations have hired firms like TigerSwan to infiltrate pipeline resistance movements.

This is not paranoia. This is documented history. Organizational OPSEC acknowledges this reality and builds structures that minimize damage when infiltration occurs — because the goal is not to achieve perfect security (impossible), but to limit the blast radius of any single compromise.

---

## 1. Structural Defenses: Building the Organization for Resilience

### 1.1 The Cellular Model

Organize sensitive work into **cells of 4–7 members** with **strict need-to-know boundaries** between them.

**How it works:**
- Each cell is functionally independent: it has its own communication channel, its own tasks, its own internal decision-making
- Cells are linked only through designated liaisons who know members on both sides
- Operational information flows only within cells, not across them, unless there is specific need
- If one cell is compromised, the others continue functioning

**Cell examples for a typical activist organization:**
- **Action Cell:** Plans and executes direct actions; knows the "who, what, when, where" of specific events
- **Logistics Cell:** Transportation, supplies, medical, finances; knows operational requirements but not always strategic details
- **Communications Cell:** Public messaging, social media, press; knows what is public, not what is operational
- **Legal Cell:** Knows participant identities and legal strategy; isolated from operational planning
- **Outreach/Recruitment Cell:** Manages new member integration; deliberately isolated from operational cells until trust is established

**Liability note:** The cellular model is not about creating hierarchy — many organizations use consensus-based decision-making within cells and between liaison representatives. The model is about *information flow*, not *power structure*.

### 1.2 Tiered Participation

Not all participation requires the same level of trust or access. Design a tiered participation model that allows people to contribute at their comfort level while controlling information access:

| Tier | Label | Access | Vetting Required |
|------|-------|--------|-----------------|
| 0 | **Public Supporter** | Public events, public materials | None |
| 1 | **Active Participant** | Internal meetings, general communications | Self-identification, one member introduction |
| 2 | **Trusted Member** | Cell membership, sensitive discussions | Two-member vouch + probationary period (2–6 months) |
| 3 | **Core Organizer** | All cell liaison roles, strategic planning | Extended trust network verification, demonstrated commitment |

**The probationary principle:** New members spend time at Tier 1 before being eligible for Tier 2. During this period, they participate fully in public-facing work, but sensitive operational discussions wait.

### 1.3 Distributed Leadership

**Single points of failure are security vulnerabilities.** An organization that depends on one or two individuals is critically vulnerable to arrest, burnout, or targeted harassment.

- Ensure every critical function has at least **two people** with the knowledge and authority to carry it out
- Document processes — not sensitively, but enough that institutional knowledge survives personnel changes
- Distribute access credentials (Signal group admin, email accounts, website admin) to multiple trusted members in documented succession
- Create and maintain a **leadership succession plan**: if your three most experienced organizers were arrested tomorrow, who takes over, and how do they access what they need?

---

## 2. Member Vetting and Trust Building

### 2.1 The Social Trust Network

The most reliable vetting mechanism is **social trust chains** — knowing a person through someone who already knows them.

**The vouch protocol:**
- New members seeking Tier 2+ access require **two existing Tier 2+ members to independently vouch** for them
- "Vouching" means: "I have known this person for [X time], in [these contexts], and I take personal responsibility for introducing them to this organization"
- Vouching is not bureaucratic — it formalizes an accountability relationship that already exists in healthy communities
- Digital-only relationships are generally insufficient for vouching. In-person knowledge matters.

**Building trust over time:**
- Consistency at public events over time is strong evidence of genuine commitment
- Demonstrating support for arrested or persecuted members is high-trust behavior
- Financial contribution (where comfortable and appropriate) indicates genuine stake

### 2.2 Red Flags and Behavioral Indicators

No single indicator is definitive. Multiple concurrent indicators warrant careful consideration and discussion.

**Possible indicators of an informant or disruptive presence:**
- **Escalation pushing:** Consistently advocates for tactics that would generate serious criminal charges; becomes frustrated when the group opts for less risky approaches
- **Selective information-seeking:** Asks detailed questions about operational specifics (names, locations, timelines) irrelevant to their stated role
- **Weak social network:** Appeared without existing connections; no one from outside the group has known them previously; refuses or is vague about providing personal background
- **Security resistance:** Frames OPSEC practices as paranoia, elitism, or excessive; resists adoption of secure communications
- **Unexplained resources:** Has financial resources, equipment, or connections inconsistent with their stated background
- **Authority-seeking:** Rapidly pursues positions of authority or access to sensitive information disproportionate to their tenure
- **Divisive behavior:** Creates or amplifies conflict between trusted members, particularly before major actions
- **Consistent unavailability:** Frequently absent at critical moments with vague explanations

**Important caveat:** These behaviors can also result from genuine personality traits, life circumstances, mental health challenges, or inexperience. **Do not accuse. Do not act unilaterally.** Bring observations to your security/leadership team for collective assessment.

### 2.3 The "60-Second Rule"

Before sharing any sensitive information in any setting, ask yourself: "If this room contained an informant, what is the damage from what I am about to say?" If the answer is significant, reconsider whether this information needs to be shared in this setting.

---

## 3. Information Security Practices

### 3.1 Secure Meeting Protocols

**Physical meetings for sensitive discussions:**
- Change locations regularly; do not meet in the same place repeatedly
- Conduct a pre-meeting device sweep: ask all attendees to place phones in Faraday bags or leave them outside the space
- Use white noise machines near windows and doors
- Brief all attendees: "This meeting is sensitive. Please do not discuss what is discussed here outside this space without explicit approval."

**Digital meeting security:**
- Use Signal for audio/video calls — end-to-end encrypted
- Do not use Zoom, Google Meet, Teams, or similar corporate platforms for sensitive discussions
- If video is needed and Signal video is insufficient (large group), use a self-hosted Jitsi instance or Jami (peer-to-peer, no central server)
- Record meetings only with explicit consent of all participants; store recordings on encrypted, local storage

### 3.2 Document Control

**For organizational documents:**
- Store sensitive documents in a zero-knowledge encrypted cloud service (Proton Drive, Cryptomator + cloud, Keybase Teams) or a locally-hosted system
- Do not use Google Docs or Microsoft 365 for sensitive organizational documents — both companies comply with law enforcement requests
- Apply the classification system from the OPSEC Principles guide (Public/Internal/Sensitive/Critical) to all documents
- Delete documents after they are no longer needed; most operational plans do not need to be stored long-term
- Maintain a "data minimization" principle: document only what is necessary for operational continuity

**For financial records:**
- Use a dedicated financial institution with progressive-organization-friendly policies
- Consider fiscal sponsorship through an established nonprofit if that adds legal protection
- Maintain clean books for legal compliance and transparency, but protect donor identities appropriately

### 3.3 Social Media Operational Security

**What to never post publicly:**
- Names or photos of participants at actions without explicit individual consent
- Real-time location information during active operations
- Internal disagreements, strategic debates, or organizational tensions
- Specific future plans, timelines, or locations before they are executed
- Information about legal strategy or ongoing legal matters
- Information about participants' immigration status, employment, or family situations

**Public persona management:**
- Your organization's public accounts should be managed by a designated communications cell member who understands what is and is not appropriate to share
- Consider whether your organization's public accounts should follow other organizations, individuals, or hashtags that could create implicit networks visible to adversaries
- Review old posts periodically for information that may have been harmless to post but now creates a trail

---

## 4. When Infiltration Is Suspected or Confirmed

### 4.1 The Process for Handling Suspicion

1. **Observe and document** concerning behaviors privately. Do not act on a hunch without evidence.
2. **Consult a small trusted circle** (2–3 core organizers). Do not broadcast suspicion widely — false accusations destroy organizations.
3. **Apply the canary trap** if appropriate: provide subtly different non-critical information to each suspected party and monitor for external surfacing.
4. **Limit access proactively** as investigation proceeds — move sensitive discussions to spaces the suspected person does not have access to. Frame this as "restructuring" if needed.
5. **Consult legal counsel** before taking any formal action. How you handle a suspected informant has legal implications.

### 4.2 After Confirmation

When an infiltrator is positively identified:

1. **Do not confront publicly or immediately.** This alerts their handlers.
2. **Conduct a damage assessment:** What did this person have access to? What operations, identities, or strategies may be known to law enforcement?
3. **Adjust all operational plans** they were aware of. Change locations, timelines, personnel assignments, and communication channels.
4. **Consult legal counsel** about exposure and next steps.
5. **Consider organizational disclosure** after legal consultation — your broader membership deserves to know, but the timing and manner matters.
6. **After the dust settles:** Do a full security audit. The infiltrator may not have been the only change; their presence may have enabled secondary surveillance.

### 4.3 Avoiding Paranoia (The Cure That Kills)

**The greatest weapon of infiltration programs is not the informant — it is the accusation.** COINTELPRO was most effective not when it planted actual informants but when it sent anonymous letters claiming trusted leaders were informants, creating suspicion and destroying relationships.

- Never act on suspicion alone
- Never make accusations publicly or without careful consultation
- Create a culture where security practices are normalized (everyone uses Signal; everyone attends security trainings) so no individual's security practices seem suspicious
- Build strong interpersonal relationships within your organization — genuine community is the most powerful defense against infiltration and the accusations it provokes

---

## 5. Long-Term Organizational Resilience

### 5.1 Security Culture as Practice

Security is not a procedure you implement — it is a culture you build. Signs of a healthy security culture:

- New members are welcomed into security practices as a normal part of onboarding, not an afterthought
- Security discussions are normalized, not stigmatized
- People feel comfortable raising concerns about potential threats without being labeled "paranoid"
- Security practices are implemented without creating a culture of fear, suspicion, or exclusion
- The organization balances security needs with the openness required for community building and growth

### 5.2 Resilience Planning

- **Suppression scenario:** If key organizers were arrested tomorrow, who leads? Where are the resources? Who has access to what?
- **Legal attack scenario:** If the organization were served with a SLAPP suit or its bank accounts frozen, what happens? Is there a backup financial institution? A legal defense plan?
- **Infiltration scenario:** If a significant breach were discovered, what is the recovery plan? How would you rebuild trust?
- **Infrastructure failure:** If your primary communication platform (Signal group, email list) were compromised or banned, what is the backup?

Document these contingency plans with your leadership team. Store them securely and accessibly.

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
