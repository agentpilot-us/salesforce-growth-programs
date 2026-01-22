# ABM New Logo Acquisition - Salesforce Agentforce Blueprint

> **Implementation Status:** Production  
> **Client Industry:** B2B SaaS (Mid-Market)  
> **Time to Complete Blueprint:** 50 minutes  
> **Implementation Timeline:** 8 weeks

---

## 1. GROWTH PROGRAM OVERVIEW

- **Program Type:** ABM - New Logo Acquisition
- **Business Objective:** Land new enterprise accounts by orchestrating multi-threaded cold outreach across buying committee
- **Target Audience:** Net-new target accounts (100 accounts, 20-30 contacts each = 2,500 contacts)
- **Success Metrics:** 
  - **Primary:** 25%+ response rate (cold outreach), $1M+ new logo pipeline per quarter, 15+ qualified meetings per month
  - **Secondary:** 4+ buying group members engaged before first meeting, 80%+ opportunities multi-threaded
  - **Tertiary:** <24 hours from intent signal to outreach, 75%+ agent draft approval rate

---

## 2. BUYER/USER JOURNEY

**Stage 1: Awareness (Intent Detected)**  
→ **Trigger:** Contact enters target account list AND shows intent signal (visits website, downloads content, researches industry)  
→ **Action:** Agent generates personalized cold outreach email referencing intent signal and industry context

**Stage 2: Problem Recognition**  
→ **Trigger:** Contact engages (opens email >2x, visits product pages, reads case studies)  
→ **Action:** Agent sends industry-specific pain point content + competitor comparison white paper

**Stage 3: Solution Education**  
→ **Trigger:** Multiple contacts from same account engage OR high-value contact downloads content  
→ **Action:** Agent drafts meeting invitation for SDR/BDR emphasizing multi-stakeholder value and social proof

**Stage 4: Qualified Opportunity**  
→ **Trigger:** 4+ buying group members engaged + meeting scheduled + budget/timeline confirmed  
→ **Action:** Create new logo opportunity in CRM, alert AE team, trigger account planning process, multi-threaded opportunity flag set

---

## 3. DATA REQUIREMENTS

### Data Sources:

- [X] **CRM** - Salesforce objects: Lead, Account, Contact, Opportunity, Campaign
- [X] **Marketing Automation** - Email engagement, content downloads, nurture track status, webinar attendance
- [X] **Intent Data Provider** - Website visits (frequency, pages, duration), content consumption (topics, depth), competitive research patterns
- [X] **Technographic Data** - Current tech stack, tools in use, integration patterns, IT budget signals
- [X] **Firmographic Data** - Company size, industry/sub-vertical, revenue, growth trajectory, funding stage

### Target Account Context Needed:

**Company Intelligence:**
- Industry & sub-vertical (specific use cases)
- Company size, employee count, growth trajectory
- Recent funding, acquisitions, leadership changes (buying signals)
- Job postings (hiring for roles related to your solution)
- Technology stack (displacement opportunity vs. greenfield)

**Competitive Context:**
- Current tools/vendors in use
- Known pain points with existing solutions
- Renewal timing (if known)
- Competitor win/loss intelligence

**Intent Signals:**
- Website behavior (pages visited, time spent, repeat visits)
- Content engagement (whitepapers, case studies, product pages)
- Search activity (topics researched, keywords)
- G2/review site activity
- Conference attendance/webinar registration

### Data Cloud Segments Needed:

1. **Segment Name:** Economic Buyer - New Logo  
   **Criteria:** VP+ title AND Budget authority AND Target account list AND (Shows intent signals in last 30 days OR Job change in last 90 days)  
   **Size:** ~500 contacts across 100 accounts

2. **Segment Name:** Technical Evaluator - New Logo  
   **Criteria:** Engineering/IT/Ops titles AND Likely tech decision-maker AND Visited technical documentation OR integration pages  
   **Size:** ~700 contacts

3. **Segment Name:** End User - New Logo  
   **Criteria:** Day-to-day user persona titles AND Engaged with use case content AND Industry-specific role  
   **Size:** ~800 contacts

4. **Segment Name:** Executive Sponsor - New Logo  
   **Criteria:** C-suite in target account AND Strategic initiative alignment (recent funding, hiring, press mentions) AND High-intent signals  
   **Size:** ~300 contacts

5. **Segment Name:** Champion (Potential) - New Logo  
   **Criteria:** Mid-level manager AND High engagement (3+ website visits, 2+ content downloads) AND Cross-functional role AND Early advocate signals  
   **Size:** ~200 contacts

---

## 4. AGENTFORCE AGENT DESIGN

**Agent Name:** "New Logo Acquisition Agent"

**Agent Purpose:** Orchestrate multi-threaded cold outreach to target accounts based on intent signals and buying group composition, generating personalized cold emails that demonstrate relevance and value.

### Agent Actions:

1. **Action:** Pull contact data  
   **From:** Data Cloud buying group segments (new logo-specific + intent criteria)  
   **Output:** Contact profile with intent signals, firmographics, tech stack

2. **Action:** Retrieve intent & firmographic data  
   **From:** Data Cloud Unified Account + Intent Signal objects  
   **Output:** Website visits, content downloads, industry context, competitive intelligence

3. **Action:** Generate personalized cold email  
   **Using:** RAG from messaging framework + intent context + industry pain points + competitive positioning  
   **Output:** 3-4 sentence permission-based cold email with intent reference

4. **Action:** Create draft task  
   **To:** SDR/BDR (primary) or AE (if strategic account)  
   **Output:** Task with draft, intent summary, account context, suggested timing

5. **Action:** Log activity  
   **To:** Lead/Contact, Campaign Member, Intent_Signal__c tracking  
   **Output:** Activity record for reporting and multi-threading visibility

6. **Action:** Check account-level engagement  
   **Logic:** If Engaged_Buying_Groups_Count__c ≥ 4 → Create Opportunity  
   **Output:** Multi-threaded opportunity with alert to AE team

### Unique Context Agent Uses:

**Intent Signal References:**
- "I noticed your team recently visited our [Product] pricing page..."
- "I saw you downloaded our whitepaper on [Topic] - that tells me [Pain Point] is top of mind..."
- "Your team has been researching [Category] solutions - here's why companies like yours choose us..."

**Firmographic Context:**
- "As a [Industry] company scaling from [Size] to [Size], you're likely facing [Pain Point]..."
- "I saw [Company] recently raised [Funding Amount] / hired a VP of [Function] / acquired [Company]..."
- "Companies in [Industry] at your stage typically struggle with [Challenge]..."

**Competitive Context:**
- "Your team is currently using [Competitor Tool] - here's how we're different on [Key Differentiator]..."
- "Many [Industry] companies switch from [Competitor] to us because..."
- "Unlike [Competitor], we offer [Unique Value Prop]..."

**Social Proof:**
- "Similar companies like [Customer A], [Customer B] switched to us and achieved [Result]..."
- "[Competitor Customer] was in your exact situation 6 months ago - here's what changed..."

### Knowledge/RAG Requirements:

**Messaging Framework (42 pages):**

**Cold Outreach Best Practices:**
- Permission-based language patterns
- Value-first opening (no asks in first email)
- Intent-signal-based personalization
- How to reference research without being creepy

**Industry-Specific Pain Points:**
- By vertical (SaaS, Manufacturing, Financial Services, Healthcare, etc.)
- By company size (SMB, Mid-Market, Enterprise)
- By growth stage (Startup, Growth, Mature)
- Current event triggers (economic changes, regulations, trends)

**New Logo Value Propositions:**
- Why switch from current solution
- Why adopt now vs. waiting
- Competitive differentiation (vs. top 3 competitors)
- ROI models for new customers
- Implementation ease for net-new deployments

**Competitive Differentiation:**
- Battle cards for top 5 competitors
- Feature comparison matrices
- Win/loss analysis insights
- Customer testimonials (former competitor customers)

**Social Proof Library:**
- Case studies by industry and company size
- G2/review site quotes
- Customer testimonial videos
- ROI achieved by similar companies

**Objection Handling (Cold Context):**
- "Why should I care?" → Value statement
- "We already have X tool" → Competitive differentiation
- "Not the right time" → Urgency creation
- "Send me info" → Meeting-first approach

---

## 5. SALESFORCE ARCHITECTURE

### Objects Used:

**Standard Objects:**
- Lead (for unknown contacts)
- Account (target account management)
- Contact (for known contacts)
- Campaign (cold outreach campaign tracking)
- Task (agent draft review queue)
- Opportunity (multi-threaded new logo opportunities)

**Custom Objects:**
- `Buying_Group__c` (junction: Account + Lead/Contact + Role + Status)
  - Fields: Account__c, Contact__c, Lead__c, Role__c, Intent_Score__c, First_Engaged__c
- `Agent_Draft__c` (stores agent-generated cold emails)
  - Fields: Lead__c, Contact__c, Draft_Content__c, Intent_Context__c, Approved__c, Sent_Date__c, Response__c
- `Intent_Signal__c` (tracks website visits, content downloads by account)
  - Fields: Account__c, Signal_Type__c (Website Visit, Content Download, Search Activity), Signal_Date__c, Page__c, Topic__c, Score__c
- `Account_Engagement_Score__c` (aggregate engagement across buying groups)
  - Fields: Account__c, Total_Intent_Score__c, Buying_Groups_Identified__c, Buying_Groups_Engaged__c, Last_Signal_Date__c

### Key Fields Added:

**Account Fields:**
- `Target_Account__c` (Boolean - on target account list)
- `Industry_Vertical__c` (Picklist with sub-verticals)
- `Intent_Score__c` (Number 0-100, composite of all signals)
- `Engaged_Buying_Groups_Count__c` (Rollup from Buying_Group__c)
- `Competitive_Tool_In_Use__c` (Text - current vendor/tool)
- `First_Intent_Date__c` (Date - when account first showed interest)
- `Multi_Threaded__c` (Boolean - 4+ buying groups engaged)

**Lead/Contact Fields:**
- `Buying_Group_Role__c` (Picklist: Economic Buyer, Technical Evaluator, End User, Executive Sponsor, Champion)
- `Intent_Signal_Type__c` (Picklist: Website Visit, Content Download, Search Activity, Webinar, Event)
- `Last_Intent_Date__c` (Date)
- `Cold_Outreach_Priority__c` (Picklist: High, Medium, Low based on intent + role)
- `Intent_Score__c` (Number 0-100)
- `Competitive_Tool_User__c` (Boolean - uses competitor)

**Opportunity Fields:**
- `Multi_Threaded__c` (Boolean - 4+ buying groups engaged)
- `Intent_Triggered__c` (Boolean - created from intent signals)
- `First_Intent_Date__c` (Date - earliest signal from account)

### Flows/Automation:

**Flow 1: "New Intent Signal Detected"**  
→ **Trigger:** Intent_Signal__c record created (from Data Cloud via Platform Event)  
→ **Criteria:** Signal_Score__c ≥ 70 AND Account is target account AND Contact/Lead has buying group role  
→ **Action:** Create Agent_Draft__c record, Create Task for SDR/BDR, Update Lead/Contact Intent_Score__c

**Flow 2: "Multi-Threaded Engagement Threshold"**  
→ **Trigger:** Buying_Group__c record updated (Status__c = "Engaged")  
→ **Criteria:** Account.Engaged_Buying_Groups_Count__c ≥ 4 AND No open opportunity exists  
→ **Action:** Create New Logo Opportunity, Set Multi_Threaded__c = TRUE, Alert AE team (Chatter + Email), Create account plan task

**Flow 3: "Agent Draft Approval - New Logo"**  
→ **Trigger:** Task status = "Completed" AND Task.Type = "Cold Outreach Draft"  
→ **Criteria:** Task.Status_Detail__c = "Approved"  
→ **Action:** Send email via Marketing Cloud or native Salesforce, Add to Campaign, Update Agent_Draft__c.Sent_Date__c, Log activity to Lead/Contact

**Flow 4: "Cold Outreach Response Handler"**  
→ **Trigger:** Task created from Email Reply (via Email-to-Case or Einstein Activity Capture)  
→ **Criteria:** Task.Subject contains "Re:" AND Related to cold outreach campaign  
→ **Action:** Update Agent_Draft__c.Response__c = TRUE, Update Buying_Group__c.Status__c = "Responded", Alert SDR/BDR, Create follow-up task

**Flow 5: "Intent Score Decay"**  
→ **Trigger:** Scheduled (nightly)  
→ **Criteria:** Last_Intent_Date__c > 30 days ago  
→ **Action:** Reduce Intent_Score__c by 10%, Update Cold_Outreach_Priority__c

### Integrations:

**Integration 1: Marketing Cloud → Data Cloud**  
→ **Purpose:** Email engagement data (sends, opens, clicks, unsubscribes) from cold outreach campaigns  
→ **Method:** Marketing Cloud Connect (native connector)  
→ **Frequency:** Real-time for engagement events

**Integration 2: Intent Data Provider (6sense, Bombora, etc.) → Data Cloud**  
→ **Purpose:** Website visit tracking, content consumption, topic research, buying stage signals  
→ **Method:** REST API batch import or streaming webhook  
→ **Frequency:** Hourly batch or real-time webhook

**Integration 3: ZoomInfo/Clearbit → Data Cloud**  
→ **Purpose:** Firmographics (company size, revenue, industry), technographics (tech stack), contact enrichment  
→ **Method:** API enrichment on new lead/contact creation  
→ **Frequency:** Real-time on record creation, monthly batch refresh

**Integration 4: Data Cloud → Salesforce CRM**  
→ **Purpose:** Real-time segment updates, intent scores, calculated insights to Lead/Contact/Account  
→ **Method:** Data Cloud Activation (native streaming)  
→ **Frequency:** Real-time

**Integration 5: G2/Review Sites → Data Cloud** (Optional)  
→ **Purpose:** Competitor research activity, review reading patterns  
→ **Method:** API integration or manual batch upload  
→ **Frequency:** Weekly batch

### Data Cloud Setup:

**Data Streams:**
1. Salesforce CRM (Lead, Account, Contact, Opportunity, Campaign Member)
2. Marketing Cloud (Email Studio engagement from cold campaigns)
3. Intent Data Provider (website activity, content consumption, search topics)
4. Firmographic Provider (company data, employee count, revenue, tech stack)
5. Website Analytics (product page visits, pricing page visits, case study views)

**Data Model Objects:**

**Unified Individual Profile:**
- Core: First Name, Last Name, Email, Phone, Title, Department, Seniority, Company
- Intent: Intent_Score, Last_Intent_Date, Intent_Signal_Types (array), Pages_Visited (array)
- Firmographic: Company_Size, Industry, Revenue_Range
- Tech Stack: Current_Tools (array), Competitive_Tool_User (boolean)
- Engagement: Email_Opens_30d, Content_Downloads_90d, Webinar_Attended

**Unified Account Profile:**
- Core: Account_Name, Industry, Sub_Vertical, Employee_Count, Revenue_Estimate
- Intent: Account_Intent_Score, First_Intent_Date, Total_Signals_Count, High_Intent_Topics (array)
- Growth Signals: Recent_Funding, Recent_Hires, Job_Postings_Count, Executive_Changes
- Tech Stack: Tools_In_Use (array), Known_Pain_Points (array)
- Engagement: Buying_Groups_Identified, Buying_Groups_Engaged, Multi_Threaded_Flag

**Calculated Insights:**

1. **Account_Intent_Score** (Number 0-100)  
   Formula: (Website_Visits × 2) + (Content_Downloads × 5) + (Pricing_Page_Visits × 10) + (Repeat_Visits × 3) + (Time_Spent_Score × 2)

2. **Buying_Group_Coverage** (Percentage)  
   Formula: (Unique Buying Group Roles Identified / 5 Target Roles) × 100

3. **Cold_Outreach_Propensity** (Number 0-100)  
   Formula: (Intent_Score × 0.4) + (Buying_Group_Role_Score × 0.3) + (Firmographic_Fit_Score × 0.2) + (Timing_Score × 0.1)

**Segments (5 core + variations):**
- Economic Buyer - New Logo (criteria in section 3)
- Technical Evaluator - New Logo
- End User - New Logo
- Executive Sponsor - New Logo
- Champion (Potential) - New Logo

Plus segment variations:
- High Intent (Intent_Score > 80)
- Competitive Displacement (Competitive_Tool_In_Use = TRUE)
- Recent Signal (Intent signal in last 7 days)
- Executive Buyer (C-suite with high intent)

---

## 6. HUMAN TOUCHPOINTS

**Review Point 1: Daily Cold Draft Review (SDRs/BDRs)**  
→ **Who:** SDRs/BDRs review agent-drafted cold emails  
→ **When:** Morning review queue (first 30 min of day)  
→ **What:** Approve, edit, or reject drafts; adjust personalization if needed; check timing appropriateness  
→ **Tool:** Task queue in Salesforce (filtered list view by owner)  
→ **SLA:** <24 hours from draft creation (especially for high-intent signals)

**Review Point 2: Multi-Threaded Opportunity Handoff (SDR → AE)**  
→ **Who:** SDR reviews opportunity with AE before first meeting  
→ **When:** When 4+ buying groups engaged + meeting scheduled  
→ **What:** Brief AE on buying group composition, intent signals, competitive context, account history  
→ **Tool:** Opportunity record + Chatter thread + Account plan document  
→ **Process:** SDR creates opportunity → Alerts AE → Handoff meeting within 24 hours

**Review Point 3: Weekly Messaging Review (Marketing + Sales)**  
→ **Who:** Marketing reviews cold messaging performance with sales team  
→ **When:** Weekly content review  
→ **What:** Review response rates by message type, approve new industry messaging, update competitive intel, refresh case studies  
→ **Tool:** Marketing dashboard + Shared messaging doc  
→ **Decisions:** What messaging to amplify, what to retire, new A/B tests

**Review Point 4: Monthly Target Account Review (Sales Leadership)**  
→ **Who:** VP Sales, Director of Sales Development, RevOps  
→ **When:** Monthly planning meeting  
→ **What:** Review target account list performance, approve new accounts for next month, adjust intent score thresholds, review win/loss  
→ **Tool:** Tableau/Salesforce dashboard showing account progression  
→ **Decisions:** Budget allocation, account prioritization, resource assignment

---

## 7. SUCCESS DASHBOARD

### Dashboard: "New Logo Acquisition Performance"

**Primary KPIs (Top Row):**
- **New Logo Pipeline Generated:** Target $1M/quarter | Current: [Live metric]
- **Cold Outreach Response Rate:** Target 25%+ | Current: [Live metric]
- **Qualified Meetings Booked:** Target 15/month | Current: [Live metric]
- **Average Buying Groups Engaged per Account:** Target 4+ | Current: [Live metric]

**Agent Performance (Second Row):**
- **Agent Drafts Generated:** [Volume] drafts/week
- **Agent Drafts Approved %:** Target 75%+ | Current: [Live metric] (lower than expansion due to cold context)
- **Intent Signal → Outreach Time:** Target <24h | Current: [Live metric]
- **Draft Edit Rate:** % requiring significant edits (quality indicator)

**Target Account Progress (Third Row - Funnel):**
- Stage 1: Target Account (No Engagement) - 100 accounts
- Stage 2: 1-2 Buying Groups Engaged - 60 accounts
- Stage 3: 3+ Buying Groups Engaged - 30 accounts
- Stage 4: Multi-Threaded (4+ Groups) - 20 accounts
- Stage 5: Opportunity Created - 15 accounts
- Stage 6: Closed-Won - 5 accounts

**Intent Signal Activity (Fourth Row - Heatmap):**
- Accounts by Intent Score (0-20: Low, 21-50: Medium, 51-80: High, 81-100: Very High)
- Intent Signals by Account (Top 20 accounts with most activity)
- Signal Type Distribution (Website Visits vs. Content Downloads vs. Search Activity)

**Multi-Threading Metrics (Fifth Row):**
- Multi-Threaded Opportunities: [Count] opportunities with 4+ engaged buying groups
- % of Opportunities Multi-Threaded: Target 80%+ | Current: [Live metric]
- Average Buying Groups at First Meeting: Target 4+ | Current: [Live metric]
- Multi-Threaded Win Rate vs. Single-Threaded: [Comparison metric]

**Trend Analysis (Bottom Row - Line Charts):**
- Pipeline created by week (last 12 weeks)
- Response rate trend by month
- Intent signals detected per week
- Agent draft volume and approval rate over time

### Reports to Build:
1. **New Logo Pipeline by Account** (Opportunity report grouped by Account, filtered by Type = "New Logo")
2. **Buying Group Coverage Matrix** (Account × Buying Group heatmap showing engagement)
3. **Cold Draft Queue** (Task report for SDRs/BDRs, filtered by Type = "Cold Outreach Draft")
4. **Intent Signal Activity** (Custom report on Intent_Signal__c showing top accounts)
5. **Multi-Threading Analysis** (Opportunity report comparing win rates by # of buying groups engaged)
6. **Response Rate by Industry** (Campaign report grouped by Industry to identify best-fit verticals)
7. **Competitive Displacement Opportunities** (Account report filtered by Competitive_Tool_In_Use__c)

---

## 8. IMPLEMENTATION TIMELINE

**Week 1-2: Data Foundation & Intent Integration**  
**Tasks:**
- Set up Data Cloud data streams (CRM, Marketing, Intent Data, Firmographics)
- Configure data model objects (Unified Individual, Unified Account)
- Build calculated insights (Account_Intent_Score, Cold_Outreach_Propensity)
- Test intent data flow and quality
- Validate firmographic enrichment

**Deliverables:** Data Cloud configured with all data sources, intent signals flowing in real-time

---

**Week 3: Target Account List & Buying Group ID**  
**Tasks:**
- Finalize target account list (100 accounts)
- Research and document ideal customer profile (ICP)
- Identify buying group members in each account (use ZoomInfo, LinkedIn)
- Import target account list to Salesforce
- Validate contact data quality

**Deliverables:** 100 target accounts loaded, ~2,500 contacts identified

---

**Week 4: Segment Creation**  
**Tasks:**
- Create 5 buying group segments with new logo + intent criteria
- Test segment population and quality
- Validate segment logic with sales team sample accounts
- Set up segment activation to Salesforce (Lead/Contact)
- Create high-intent variations (Intent_Score > 80)

**Deliverables:** 5 segments active, documented criteria, intent-based prioritization working

---

**Week 5: Messaging Framework Development**  
**Tasks:**
- Document cold outreach best practices and permission-based language
- Research and document industry-specific pain points (top 5 verticals)
- Create new logo value propositions and competitive differentiation
- Compile social proof library (case studies by industry)
- Structure objection handling for cold context
- Get sales/marketing approval on messaging
- Upload to Data Cloud Knowledge for RAG

**Deliverables:** 42-page cold outreach messaging framework stored in Data Cloud

---

**Week 6: Agentforce Agent Build**  
**Tasks:**
- Configure Agentforce agent with cold outreach instructions and actions
- Integrate RAG (connect to Data Cloud Knowledge)
- Set up intent signal retrieval logic
- Build competitive intelligence lookup (current tools → our differentiation)
- Test agent with 20 sample contacts (4 from each buying group)
- Refine prompts based on test output quality

**Deliverables:** Agentforce agent operational, cold drafts passing quality review

---

**Week 7: Salesforce Configuration & Testing**  
**Tasks:**
- Create custom objects (Buying_Group__c, Agent_Draft__c, Intent_Signal__c, Account_Engagement_Score__c)
- Build flows (intent signal trigger, draft approval, multi-threading threshold)
- Configure dashboard and reports
- Create task views for SDRs/BDRs
- Set up campaign tracking structure
- End-to-end testing with 10 pilot accounts

**Deliverables:** Full system integrated, all flows tested, dashboard operational

---

**Week 8: SDR Enablement & Pilot Launch**  
**Tasks:**
- Train SDRs/BDRs on cold draft review process and approval workflow
- Document cold outreach playbook and FAQs
- Set expectations on response rates (25% target for cold)
- Launch pilot with 10 target accounts (highest intent)
- Monitor daily for first week, troubleshoot issues
- Gather feedback from SDR team on draft quality

**Deliverables:** Pilot live with 10 accounts, documented learnings, draft quality validated

---

**Week 9-10: Scale & Optimize**  
**Tasks:**
- Week 9: Roll out to 30 additional accounts (40 total)
- Week 10: Roll out to all 100 target accounts
- Monitor KPIs daily (response rate, intent signal → outreach time)
- Weekly review of response rates and adjust messaging
- A/B test different opening lines and intent references
- Optimize segment criteria based on engagement data

**Deliverables:** Full program at scale (100 accounts), optimization playbook

---

**Ongoing: Continuous Improvement**  
**Tasks:**
- Weekly messaging review and updates
- Monthly target account list refresh (add/remove accounts)
- Quarterly competitive intelligence update
- Regular intent threshold optimization
- Win/loss analysis to refine ICP

**Total Timeline:** 8 weeks to pilot, 10 weeks to full scale

---

## 9. REUSABLE COMPONENTS FROM LIBRARY

**From universal-components:**
- [X] `Buying_Group__c` custom object schema → Reuse 90% (add Intent_Score__c field)
- [X] `Agent_Draft__c` custom object schema → Reuse 100%
- [X] Segment-to-Task flow template → Adapt trigger to intent signals
- [X] Program performance dashboard → Customize for cold outreach KPIs

**From adaptable-components:**
- [X] Unified Individual profile template → Add intent signal fields, tech stack fields
- [X] Unified Account profile template → Add intent score, growth signals, competitive context
- [X] Segment criteria patterns → Adapt for new logo + intent thresholds
- [X] Agent configuration template → Customize for cold context + intent references

**From program-implementations/abm-expansion:**
- [X] Buying group framework (5 roles) → Same roles, different criteria
- [X] Agent architecture (Pull → Generate → Task → Log) → Reuse flow, change context
- [X] Dashboard structure → Adapt KPIs for cold vs. warm

**New/Program-Specific Components:**
- `Intent_Signal__c` custom object
- `Account_Engagement_Score__c` custom object
- Intent data integration (6sense, Bombora, etc.)
- Cold outreach messaging framework (42 pages, different from expansion)
- Competitive intelligence lookup logic
- Multi-threading threshold logic (4+ vs. 3+)
- Intent signal decay flow

---

## 10. NOTES & DECISIONS

### Technical Decisions:

**Why Intent Data Integration:**
Cold outreach without intent signals = 5-8% response rate. With intent signals = 20-25% response rate. Intent data is essential for cold context to achieve acceptable performance.

**Why 4+ Buying Groups for Opportunity Creation (vs. 3+ in Expansion):**
New logo deals are harder and longer. Data shows 4+ engaged buying groups increases new logo close rate from 15% to 45%. Higher bar is justified for cold audience.

**Why Human Review for All Cold Drafts:**
Cold outreach requires perfect timing and tone. One bad email can burn an account. 100% human review maintains quality and protects brand reputation in cold context.

**Why Multi-Threaded Focus:**
Single-threaded cold outreach closes at 10% rate. Multi-threaded (4+ groups) closes at 45%. Entire program designed to force multi-threading before opportunity creation.

### Program Decisions:

**Why 100 Target Accounts (Not 500):**
Quality over quantity for new logo. 100 accounts with deep research and multi-threading outperforms 500 accounts with shallow outreach. Focus drives results.

**Why Intent-Triggered Outreach:**
Cold email without intent = spam. Intent signal = permission to engage. Program philosophy: "We only reach out when you're actively researching."

**Why Industry-Specific Messaging:**
Generic cold email fails. Industry-specific pain points (researched per vertical) drive relevance and response rates. Investment in vertical messaging pays off in 2-3x higher engagement.

### Risks & Mitigations:

**Risk:** Intent data quality issues (false positives, stale signals)  
**Mitigation:** Intent score thresholds (only act on 70+), signal decay logic (reduce score after 30 days), human validation of high-value accounts

**Risk:** SDRs overwhelmed with draft queue (bottleneck)  
**Mitigation:** Prioritization logic (high intent first), SLA tracking, gamification, capacity planning (max 20 drafts per SDR per day)

**Risk:** Competitive intelligence outdated (wrong tool in use)  
**Mitigation:** Monthly competitive data refresh, sales feedback loop, multiple data sources (ZoomInfo + Clearbit + manual research)

**Risk:** Multi-threading takes too long (accounts go cold)  
**Mitigation:** Intent signal velocity tracking, automated alerts when 3+ groups engaged, SDR playbook for accelerating engagement

---

**Blueprint Completed By:** Michelle Bastelier, Agentforce Specialist  
**Date:** January 2025  
**Next Step:** Begin Data Cloud setup and intent data integration (Week 1)  
**Estimated ROI:** $1M+ pipeline per quarter, 25%+ response rate, 4+ buying groups engaged per account, 80%+ multi-threaded opportunities

---

**Questions or feedback on this implementation?**  
Contact: michelle@agentpilot.us
