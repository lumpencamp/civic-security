# Financial Privacy: Protecting Your Money and Your Associations

*Status: Level 2 | Audience: Organizers, donors, and anyone managing organizational finances*

Financial transactions create a detailed record of your associations, movements, and activities. Every credit card swipe, digital payment, and bank transfer is logged, retained, and potentially available to law enforcement through subpoena without your knowledge. This guide covers practical strategies for financial privacy, from everyday cash use to cryptocurrency for donations.

---

## 1. Why Financial Privacy Matters for Activists

Financial records have been used to:
- Identify members of organizations through donation records subpoenaed from payment processors
- Track organizers' movements through credit card transactions at specific locations
- Freeze organizational bank accounts during legal attacks (SLAPP suits, asset freezes)
- Build cases against organizations through financial pattern analysis
- Identify confidential donors who wished to remain anonymous

**Key legal point:** Financial records held by banks and payment processors are generally accessible to law enforcement with a subpoena — no warrant required. Unlike the contents of your phone (which requires a warrant under *Riley v. California*), your bank records are held by a third party, and the "third party doctrine" significantly weakens your Fourth Amendment protection.

---

## 2. Cash: The Most Reliable Privacy Tool

Cash is:
- Untraceable once withdrawn (cash transactions leave no ongoing record)
- Accepted everywhere
- Legal for any legitimate purpose
- Not subject to payment processor account closures or freezes

### 2.1 Operational Cash Practices

- **ATM withdrawals from cash:** Withdraw cash in amounts and at times that do not create a pattern matching your operational activities. Spread withdrawals across different ATMs.
- **Pay for operational expenses in cash:** Transportation (bus, train — avoid rideshares), food during actions, emergency supplies, protest gear
- **Avoid patterns:** If you always withdraw $200 every Friday before a protest Saturday, that pattern is visible in your bank records

### 2.2 Cash for Procurement

When procuring operational equipment (burner phones, Faraday bags, encrypted drives):
- Use cash at physical stores
- Do not use store loyalty cards, which link purchases to your identity even with cash

---

## 3. Privacy-Preserving Digital Payments

Sometimes cash is not practical. These tools provide varying degrees of privacy for digital transactions.

### 3.1 Privacy.com Virtual Cards

**Privacy.com** creates virtual Visa cards that:
- Can be used for online purchases without revealing your actual bank card number
- Can be set to a merchant-locked (one merchant only) or category-locked card
- Can be set to a spending limit
- Can be paused or closed at any time

**Privacy level:** The merchant sees only the virtual card number, not your real card. However, Privacy.com itself knows your real identity (required by banking law), so this protects against data breaches at merchants but does not provide anonymity from law enforcement subpoenas to Privacy.com.

**Funding:** Privacy.com requires linking a real bank account or debit card. You can fund it with cash-purchased prepaid debit cards for an additional layer, though this has limits.

**Best use:** Protecting your real financial information from commercial data breaches, not from law enforcement.

### 3.2 Prepaid Gift Cards

Cash-purchased prepaid Visa/Mastercard gift cards can be used for online purchases, providing a layer of separation from your bank account.

**Limitations:**
- Many online merchants block or restrict gift card payments
- Gift cards often require registration (entering a name and address) for online use; use a mail service address
- Gift cards are a one-time tool; they cannot be reloaded

---

## 4. Cryptocurrency for Donations and Organizational Funding

### 4.1 Bitcoin: Not Private By Default

Bitcoin is often misconceived as anonymous. It is **pseudonymous**, not anonymous:
- Every transaction is recorded on the public blockchain permanently
- If your Bitcoin address is ever linked to your real identity (through an exchange, a purchase, or an OSINT connection), that link enables tracing of all transactions to and from that address
- Law enforcement has sophisticated blockchain analysis tools (Chainalysis, CipherTrace) that can trace Bitcoin flows across exchanges

**Do not use Bitcoin for sensitive donations if anonymity is required.** It is substantially less private than cash.

### 4.2 Monero: Designed for Privacy

**Monero (XMR)** is a cryptocurrency specifically engineered for privacy:
- **Ring Signatures:** Each transaction is signed by a ring of possible signers — it is mathematically impossible to determine which member of the ring actually signed
- **Stealth Addresses:** A one-time address is created for each transaction; linking transactions to a specific wallet is computationally infeasible
- **RingCT (Confidential Transactions):** Transaction amounts are hidden

**Practical result:** Monero transactions are not traceable on the blockchain by any currently known method. The IRS has funded research into Monero tracing and has publicly acknowledged its difficulty.

**Limitations:**
- Obtaining Monero requires either mining it (impractical for most) or converting from another currency through an exchange
- Exchanges that convert Bitcoin or fiat to Monero may require identity verification (KYC) — this creates a link from your identity to your Monero wallet, though not to subsequent transactions
- Some regulated exchanges have delisted Monero due to regulatory pressure

**Best practices for Monero:**
- Use a non-custodial wallet: Feather Wallet (desktop), Cake Wallet (mobile)
- Purchase through a KYC-free exchange where available, or through peer-to-peer exchanges
- Use a new address for each transaction (Monero does this automatically)

### 4.3 Organizational Crypto Fundraising

If your organization receives cryptocurrency donations:
- For maximum donor privacy, accept Monero
- For broader accessibility, accept Bitcoin while being transparent with donors that Bitcoin donations are not private
- Use a non-custodial wallet the organization controls — do not use exchange-hosted wallets (exchange accounts are subpoenable)
- Consult a tax attorney about reporting requirements; cryptocurrency donations to nonprofits have specific IRS reporting obligations

---

## 5. Organizational Financial Security

### 5.1 Separating Organizational and Personal Finances

- Maintain dedicated organizational bank accounts separate from any personal accounts
- Use a business checking account under the organization's legal entity name (LLC, nonprofit, unincorporated association)
- Never commingle personal and organizational funds

### 5.2 Protecting Against Account Closures

Banks and payment processors can and do close accounts of activist organizations:
- Maintain relationships with **mission-aligned financial institutions** (credit unions with explicit community/progressive values, CDFIs)
- Maintain backup accounts at a different institution — if your primary account is closed, you can pivot immediately
- Maintain a cash reserve outside the banking system for emergency operational expenses

**Alternatives to traditional banks:**
- Credit unions with community development missions
- Amalgamated Bank (explicitly mission-aligned for labor and social movements)
- Local community development financial institutions (CDFIs)

### 5.3 Fiscal Sponsorship

If your organization does not want to manage its own nonprofit status, **fiscal sponsorship** allows you to receive tax-deductible donations through an established 501(c)(3):
- The fiscal sponsor takes a percentage (typically 5–10%) for administrative handling
- The fiscal sponsor's bank account holds the funds — their legal entity, their account
- This adds a layer between your organization and the banking system

Common fiscal sponsors for progressive organizations: Tides Foundation, IOBY, Fractured Atlas (arts-focused).

**Privacy consideration:** The fiscal sponsor knows your identity and organizational details. This is less relevant for legal protection but is relevant for OSINT defense.

### 5.4 Protecting Donor Privacy

Donors who support controversial organizations face harassment and retaliation risks:
- Store donor information with the same security standards as other sensitive organizational data — encrypted, need-to-know
- Consider whether donor names need to be stored at all for small donors (beyond what accounting/legal requires)
- If accepting online donations, use a payment processor with strong privacy commitments; avoid platforms that may share donor information broadly
- For high-profile or at-risk donors, discuss a vehicle that minimizes their public exposure (donor-advised funds, fiscal sponsorship, in-kind contributions)

---

## 6. Financial Intelligence: Understanding What You're Defending Against

### 6.1 Bank Secrecy Act and SAR Reports

Banks are required by law to file **Suspicious Activity Reports (SARs)** with FinCEN (Financial Crimes Enforcement Network) for:
- Transactions of $10,000+ in cash (Currency Transaction Reports — automatic, not discretionary)
- Any pattern of transactions that seems designed to avoid reporting thresholds ("structuring")
- Any transaction associated with suspected illegal activity

**Practical implication:** Repeated cash withdrawals under $10,000 specifically to avoid reporting (structuring) is itself a federal crime. Withdraw cash in normal patterns consistent with your legitimate financial activity.

### 6.2 FARA and Organizational Financing

If your organization receives foreign funding, **Foreign Agent Registration Act (FARA)** requirements may apply. FARA compliance is separate from privacy considerations but interacts with them — FARA registrations are public records. Consult a lawyer if your organization has any international funding.

### 6.3 IRS 990 Public Disclosure

Nonprofit 501(c)(3) and 501(c)(4) organizations are required to file Form 990, which is publicly available and discloses:
- Total revenues, expenses, assets
- Officer names and compensation
- Program descriptions
- Large contractor payments

**Schedule B (donor list):** 501(c)(3) organizations must file Schedule B listing large donors, but this schedule is confidential to the IRS and **is not required to be disclosed publicly**. The Supreme Court in *Americans for Prosperity Foundation v. Bonta* (2021) affirmed that mandatory public disclosure of Schedule B would burden First Amendment rights.

---

*This guide does not constitute legal or financial advice. Cryptocurrency regulations change rapidly. Consult a licensed attorney or financial advisor for your specific situation.*

[← Back to Index](../index.md)
