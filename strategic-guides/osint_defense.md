# OSINT Defense: Protecting Your Digital Footprint

*Status: Level 2 | Audience: Organizers, Public Spokespeople, and Anyone Facing Doxxing Risk*

Open-Source Intelligence (OSINT) is the collection of information from publicly available sources — Google, social media, data brokers, public records, LinkedIn, court filings, property records, and more. It requires no hacking, no legal authority, and no special technology: just persistence, time, and freely available tools. Adversaries at every tier use OSINT. This guide teaches you to reduce your OSINT footprint systematically.

> **Key insight:** You cannot become invisible online, but you can become expensive to target. If an adversary must spend 10 hours to find your home address instead of 10 minutes, most T1 adversaries will give up and move on. Meaningful friction is achievable.

---

## 1. Understanding Your Current Exposure

Before you can reduce your footprint, you must understand it.

### 1.1 Google Yourself

Start with a comprehensive self-audit:

1. **Google your full name** in quotes (`"First Last"`), then add combinations: `"First Last" Chicago`, `"First Last" activist`, your username, your employer name
2. **Google your phone number:** Just your number, no formatting, in quotes
3. **Google your home address:** `"123 Main St Chicago"` — this often reveals property records, business registrations, court filings
4. **Google your email address:** This links your email to any publicly visible profiles, forum posts, or databases that publish it
5. **Google your username(s):** Any username you've used publicly — forums, Reddit, gaming, old blogs

**Document everything you find.** Create a spreadsheet: what was found, where, and what priority to address first.

### 1.2 Reverse Image Search

If you have photos of yourself publicly associated with your activism:
- Upload them to Google Images, TinEye, and PimEyes (a facial recognition reverse image search)
- PimEyes is particularly powerful — it finds faces across the web, including surveillance footage in some cases
- Use PimEyes to understand your exposure before adversaries do

### 1.3 Data Broker Audit

Data brokers are companies that aggregate personal information from public records, surveys, and commercial data and sell it. Major brokers include:
- Spokeo, WhitePages, Intelius, BeenVerified, Radaris, TruthFinder, Pipl
- FamilyTreeNow (particularly detailed for family connections)
- MyLife, PeopleFinder, Instantcheckmate

Search for yourself on each of these. What they have is what adversaries have.

---

## 2. Data Broker Opt-Outs

Data broker opt-out is the highest-impact OSINT defense action available to most people. It is tedious but effective.

### 2.1 Manual Opt-Outs

Each data broker has an opt-out process. Most require:
- Submitting your name and identifying information to be removed (ironic but necessary)
- Waiting 30–60 days for removal
- Repeating the process — brokers re-aggregate data from their sources, and your information will likely reappear within 6–12 months

**Priority opt-out list:**
1. Spokeo: spokeo.com/optout
2. WhitePages: whitepages.com/suppression_requests
3. BeenVerified: beenverified.com/opt-out
4. Intelius: intelius.com/opt-out
5. Radaris: radaris.com/ng/public/profile/remove
6. TruthFinder: truthfinder.com/opt-out
7. Instantcheckmate: instantcheckmate.com/opt-out
8. MyLife: mylife.com/optout
9. FamilyTreeNow: familytreenow.com/optout

**Nationwide resource:** The Privacy Rights Clearinghouse maintains a comprehensive opt-out guide at privacyrights.org/data-broker-opt-out.

### 2.2 Automated Opt-Out Services

If you cannot complete manual opt-outs, automated services do it for you (with recurring removal as data reappears):

- **DeleteMe:** ~$129/year per person; comprehensive broker removal, publishes verification reports
- **Kanary:** Alternative with good coverage
- **Mozilla Monitor Plus:** Newer option from Mozilla Foundation, integrated with Firefox

**Limitation:** No automated service covers every broker, and brokers constantly add new aggregation sources. Automated removal is a supplement to, not a replacement for, manual priority opt-outs.

### 2.3 Google Search Result Removal

Google allows you to request removal of certain personal information from search results:
- Home address, phone number, email address
- Login credentials
- Images of minors
- Non-consensual intimate images

Submit removal requests at myaccount.google.com/data-and-privacy or via the direct removal tool at support.google.com/websearch/troubleshooter/9685456.

**Note:** This removes the search result, not the underlying page. Contact the hosting site directly to remove the source.

---

## 3. Social Media Hardening

### 3.1 Audit Your Public Profiles

For each social media account:
- Review what is publicly visible (profile photo, name, bio, posts)
- Review who you follow and who follows you — these social graphs are public by default on most platforms
- Review tagged photos — photos others have tagged you in that you did not post

### 3.2 Platform-Specific Actions

**Facebook:**
- *Privacy Settings → Your Activity → Who can see your future posts → Friends* (or *Only Me* for maximum privacy)
- *Privacy Settings → How People Find and Contact You → Who can look you up using your phone number → Only Me*
- *Settings → Privacy → Your Facebook Information → Off-Facebook Activity → Clear History* — and disable future off-Facebook activity tracking
- Remove your phone number and email from your public profile
- Review and remove old posts that reveal location, associations, or information you wouldn't want surfaced now

**Instagram:**
- Switch to private account: *Settings → Account Privacy → Private Account*
- Remove or hide tagged photos: *Your Profile → Photos → [photo] → ⋯ → Hide Photo*
- Disable: *Settings → Ads → Ad Preferences → Instagram Ads → Data About Your Activity From Partners*

**Twitter/X:**
- Make protected/private if possible for sensitive users
- Remove phone number: *Settings → Account Information → Phone*
- Disable location data: *Settings → Privacy and Safety → Location Information*

**LinkedIn:**
- *Settings → Visibility → Edit your public profile* — reduce what's visible to non-connections
- Remove your phone number and exact address
- Disable: *Settings → Data Privacy → Job Seeking Preferences → Signal your interest to recruiters* (this broadcasts your information to third parties)
- Consider whether LinkedIn is necessary for your situation — it is one of the most detailed public profiles available about most professionals

### 3.3 Username Consistency Across Platforms

- Do not reuse usernames across platforms that you want kept separate
- Different usernames prevent trivial correlation between your activist accounts and personal accounts
- Use Namechk.com or KnowEm.com to identify where a username appears across platforms — then decide whether to claim and blank those accounts or leave them

---

## 4. Account Removal and Data Minimization

### 4.1 Delete Old Accounts

Old accounts from years past accumulate data breaches, forgotten posts, and identity correlations you've forgotten about.

- **JustDeleteMe.com:** A directory of direct links to deletion pages for hundreds of services, with a difficulty rating
- Delete accounts you no longer use actively
- Where deletion is not possible, archive and lock down the account (private, remove personal info, change the username to something generic)

### 4.2 Email Address Hygiene

- Use a **different email address for activism than for personal life**
- Create a dedicated email address at a privacy-respecting provider (Proton Mail, Tutanota) for organizational sign-ups and communications
- Use **email aliases** (SimpleLogin, AnonAddy) for signing up to services — each service gets a unique alias address. If that alias starts receiving spam, you know which service sold your data. Deactivate the alias to stop it.

### 4.3 Phone Number Hygiene

- **Do not give your real phone number to apps or services unless legally required or operationally necessary**
- Use a VOIP number (Google Voice, MySudo, JMP.chat) for service sign-ups
- Remove your phone number from existing accounts where possible
- Some services use phone numbers as account recovery — replace with TOTP authentication and remove the phone number after (check that the account remains accessible)

---

## 5. Physical World OSINT Reduction

Digital footprint is only half the picture. Physical records also feed OSINT databases.

### 5.1 Voter Registration

In most U.S. states, voter registration records are public and include your name, home address, and party affiliation. Some states sell this data to commercial brokers.

- Check your state's rules on voter registration privacy at ncsl.org
- Many states allow confidential registration for domestic violence survivors, crime victims, or in some states activists — check if your state has an "Address Confidentiality Program"
- In states that permit it, use a P.O. Box or mail service address for voter registration (check legality in your state)

### 5.2 Property Records

If you own property, your name and property address are public records in all U.S. states.

- If possible, consider holding property through an LLC or trust for privacy (has tax and legal implications — consult an attorney)
- If renting, your landlord's name and your approximate address may still appear in data broker aggregations

### 5.3 Business and Professional Registrations

- Business registrations (Secretary of State filings) are public records including the registered agent address
- Use a registered agent service instead of your home address for any business filings
- Nonprofit 990 tax filings are public and include officer names and sometimes addresses — use your organization's address, not your home address, for any official filings

### 5.4 Court Records

Court filings (civil suits, small claims, traffic violations, criminal matters) are generally public records and frequently appear in data broker aggregations. Limited options:
- Many courts allow sealing of records for sensitive matters — consult an attorney
- Traffic violations often appear and cannot be sealed
- Minimize frivolous litigation that generates additional records

---

## 6. Defensive OSINT: Monitoring Your Own Exposure

Once you've reduced your footprint, set up monitoring to detect when new information surfaces.

### 6.1 Google Alerts

Set up Google Alerts (google.com/alerts) for:
- Your full name in quotes
- Your known usernames
- Your organization's name
- Your home address

Alerts will email you when new content matching these terms appears in Google's index.

### 6.2 Have I Been Pwned

Sign up for breach notifications at haveibeenpwned.com — you'll be notified if your email appears in a newly discovered data breach.

### 6.3 Regular Re-Audits

Repeat the initial OSINT audit (Section 1) every 6 months. New data sources appear constantly, and existing brokers re-aggregate data after you opt out. Treatment is continuous, not one-time.

---

## 7. Protecting Family and Associates

OSINT adversaries will target people connected to you to find information they cannot find about you directly — family members (especially parents, siblings, partners), employers, and close friends.

- **Warn key family members:** Tell your closest family that you may be a target of online research and they may be contacted. What they should say: nothing beyond confirming they are not you. Provide NLG contact info if they are harassed.
- **Do not tag family members** in photos connected to your activist accounts
- **Do not mention family members' workplaces, routines, or identifying information** in any public context connected to your activist identity
- **Reduce your association in social graph data:** Review Facebook friends lists, Instagram followers, and LinkedIn connections. Are there connections that link your activist and personal identities?

---

*This guide does not constitute legal advice. Laws vary by jurisdiction.*

[← Back to Index](../index.md)
