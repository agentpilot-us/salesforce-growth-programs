# ABM Account Expansion - Salesforce Agentforce Blueprint

> **Implementation Status:** Production  
> **Client Industry:** Enterprise Technology (Fortune 100)  
> **Time to Complete Blueprint:** 45 minutes  
> **Implementation Timeline:** 6-8 weeks

---

## 1. GROWTH PROGRAM OVERVIEW

- **Program Type:** ABM - Install Base Expansion
- **Business Objective:** Expand revenue in existing accounts by activating untapped buying groups
- **Target Audience:** Contacts in strategic accounts (200 accounts, 30-50 contacts each = 10,000 contacts)
- **Success Metrics:** 
  - **Primary:** 30%+ response rate, $500K+ expansion pipeline per quarter, 20+ meetings booked per month
  - **Secondary:** 3+ buying groups engaged per account, 60-day average time to expansion opportunity
  - **Tertiary:** 80%+ agent draft approval rate, <24 hours from segment entry to outreach

---

## 2. BUYER/USER JOURNEY

**Stage 1: Discovery**  
→ **Trigger:** Contact enters new buying group segment in existing account (not currently engaged)  
→ **Action:** Agent generates personalized awareness email highlighting relevant use case based on their role and existing customer relationship

**Stage 2: Education**  
→ **Trigger:** Contact engages (opens email >2x, visits product page, downloads content)  
→ **Action:** Agent sends case study from similar role/company + ROI calculator personalized to their department

**Stage 3: Conversation**  
→ **Trigger:** Contact downloads content, replies to email, or books meeting link  
→ **Action:** Agent drafts meeting invitation for account rep to review/send, includes account context and value proposition

**Stage 4: Expansion Opportunity**  
→ **Trigger:** 3+ buying group members engaged from same account + meeting scheduled  
→ **Action:** Create expansion opportunity in CRM, alert account team, trigger account plan review

---

## 3. DATA REQUIREMENTS

### Data Sources:

- [X] **CRM** - Salesforce objects: Account, Contact, Opportunity, Product2, Asset (current products)
- [X] **Marketing Automation** - Email engagement history, content downloads, nurture track status
- [X] **Product Usage** - Current product adoption, feature usage frequency, seat count, license utilization
- [X] **Intent Signals** - Website activity on product/use case pages, competitor research patterns

### Contextual Data Needed:

**Account Context:**
- Current products purchased and implementation date
- Contract value, renewal date, and account health score
- Existing relationships (who's already engaged, champion identification)
- Past purchase history and expansion patterns
- Support ticket volume and satisfaction scores

**Contact Context:**
- Role, seniority, department alignment
- Engagement history with existing product
- Relationship to current champion/buyer
- Pain points specific to their function

**Expansion Signals:**
- Product usage indicating need for additional features
- Job postings for roles that use expanded products
- Budget cycles and approval processes
- Competitive intelligence (using competitor tools)

### Data Cloud Segments Needed:

1. **Segment Name:** Economic Buyer - Expansion  
   **Criteria:** VP+ title AND Budget authority AND NOT currently engaged in last 180 days AND Same department as existing buyer OR related function  
   **Size:** ~800 contacts across 200 accounts

2. **Segment Name:** Technical Evaluator - Expansion  
   **Criteria:** Engineering/IT/Ops titles AND Influences technical decisions AND Account has technical products AND NOT primary technical contact  
   **Size:** ~1,200 contacts

3. **Segment Name:** End User - Expansion  
   **Criteria:** Day-to-day user titles AND Department could benefit from additional products AND NOT active product user  
   **Size:** ~1,500 contacts

4. **Segment Name:** Executive Sponsor - Expansion  
   **Criteria:** C-suite AND Strategic alignment role (CFO, COO, CIO) AND Account contract value >$100K  
   **Size:** ~400 contacts

5. **Segment Name:** Influencer - Expansion  
   **Criteria:** High engagement history (email opens >60%, content downloads) AND Internal advocate signals (shares content, attends events) AND Cross-functional role  
   **Size:** ~600 contacts

---

## 4. AGENTFORCE AGENT DESIGN

**Agent Name:** "Account Expansion Outreach Agent"

**Agent Purpose:** Identify untapped buying groups in strategic accounts and generate personalized outreach that references the existing customer relationship and demonstrates value for their specific role.

### Agent Actions:

1. **Action:** Pull contact data  
   **From:** Data Cloud buying group segments (expansion-specific criteria)  
   **Output:** Contact profile with role, engagement history, account context

2. **Action:** Retrieve account context  
   **From:** Salesforce CRM (Account, Opportunity, Asset objects)  
   **Output:** Current products, contract value, existing relationships, account health

3. **Action:** Generate personalized email  
   **Using:** RAG from messaging framework + account context + role-specific value props  
   **Output:** 3-4 sentence email with account-specific references

4. **Action:** Create draft task  
   **To:** Account owner (primary) or Account team member (if owner unavailable)  
   **Output:** Task with draft email, contact context, approval workflow

5. **Action:** Log activity  
   **To:** Campaign member, Task, Contact activity timeline  
   **Output:** Tracking record for reporting and attribution

### Unique Context Agent Uses:

**Account Relationship References:**
- "Your team is already using [Product X] to [achieve Y result]..."
- "Since [Existing Champion Name] implemented [Solution] in [Department], they've achieved [Metric]..."
- "We've been working with [Company] for [X years/months] and have helped your [Department] achieve..."

**Cross-sell/Upsell Context:**
- "Based on your current [Product A] usage, [Product B] could help your team..."
- "With your upcoming renewal in [Month], this is a great time to explore..."
- "Teams similar to yours typically expand into [Solution] within [Timeframe]..."

**Role-Specific Personalization:**
- Economic Buyer: ROI, budget efficiency, cost avoidance
- Technical Evaluator: Integration ease, scalability, technical specs
- End User: Productivity gains, ease of use, daily workflow impact
- Executive Sponsor: Strategic alignment, competitive advantage, risk mitigation

### Knowledge/RAG Requirements:

**Messaging Framework (38 pages):**

**Expansion-Specific Pain Points:**
- By persona (Economic Buyer, Technical, End User, Executive, Influencer)
- By current product (what problems still exist)
- By industry/vertical (specific expansion challenges)

**Cross-sell/Upsell Value Propositions:**
- Feature gap analysis (what they're missing)
- Competitive differentiation (why expand vs. switch)
- Bundle pricing benefits
- Implementation ease (already integrated)

**Customer Success Stories:**
- Similar expansion journeys
- ROI achieved within 30/60/90 days
- Use cases by role and department

**ROI Models:**
- Cost per additional seat
- Feature value quantification
- Time savings calculations
- Risk reduction metrics

**Supporting Content Library:**
- Product documentation for expansion products
- Integration guides (already set up)
- Competitive battle cards
- Objection handling scripts

---

## 5. SALESFORCE ARCHITECTURE

### Objects Used:

**Standard Objects:**
- Account, Contact, Campaign, Task, Opportunity, Product2, Asset (current products), OpportunityLineItem
- Campaign (expansion campaign tracking)
- Task (agent draft review queue)

**Custom Objects:**
- `Buying_Group__c` (junction: Account + Contact + Role + Status)
  - Fields: Account__c, Contact__c, Role__c (picklist), Engagement_Score__c, Last_Engaged__c
- `Agent_Draft__c` (stores agent-generated content before approval)
  - Fields: Contact__c, Draft_Content__c, Context_Used__c, Approved__c, Sent_Date__c, Response__c
- `Account_Expansion_Signal__c` (tracks engagement across buying groups)
  - Fields: Account__c, Buying_Groups_Engaged__c, Expansion_Score__c, Last_Signal_Date__c, Signal_Type__c

### Key Fields Added:

**Account Fields:**
- `Current_Products__c` (Multi-select picklist or related Asset records)
- `Contract_Value__c` (Currency)
- `Expansion_Opportunity_Score__c` (Formula: engagement + product usage + account health)
- `Engaged_Buying_Groups__c` (Rollup count from Buying_Group__c)
- `Renewal_Date__c` (Date)
- `Account_Health_Score__c` (Number 0-100)

**Contact Fields:**
- `Buying_Group_Role__c` (Picklist: Economic Buyer, Technical Evaluator, End User, Executive Sponsor, Influencer)
- `Expansion_Priority__c` (Picklist: High, Medium, Low based on engagement + intent)
- `Current_Product_User__c` (Boolean - actively using products)
- `Last_Expansion_Outreach__c` (Date)
- `Expansion_Engagement_Score__c` (Number 0-100)

### Flows/Automation:

**Flow 1: "New Contact in Expansion Segment"**  
→ **Trigger:** Contact enters Data Cloud segment (Platform Event from Data Cloud)  
→ **Criteria:** Contact not engaged in last 180 days AND Account is strategic  
→ **Action:** Create Agent_Draft__c record, Create Task for account owner, Update Contact status

**Flow 2: "Buying Group Engagement Threshold"**  
→ **Trigger:** Buying_Group__c record updated (engagement score changes)  
→ **Criteria:** Count of engaged contacts in account ≥ 3 AND Multiple buying groups represented  
→ **Action:** Create Expansion Opportunity, Alert account team (Chatter/Email), Update Account_Expansion_Signal__c

**Flow 3: "Agent Draft Approval"**  
→ **Trigger:** Task status = "Completed" AND Task.Type = "Agent Draft Review"  
→ **Criteria:** Task.Status_Detail__c = "Approved"  
→ **Action:** Send email (Email Alert), Add to Campaign, Update Agent_Draft__c.Sent_Date__c, Log activity

**Flow 4: "Expansion Opportunity Nurture"**  
→ **Trigger:** Opportunity.Stage = "Expansion - Nurture"  
→ **Criteria:** No activity in 14 days  
→ **Action:** Create task for account owner, Trigger re-engagement sequence

### Integrations:

**Integration 1: Marketing Cloud → Data Cloud**  
→ **Purpose:** Email engagement data (opens, clicks, unsubscribes)  
→ **Method:** Marketing Cloud Connect (native connector)  
→ **Frequency:** Real-time for opens/clicks, batch daily for historical

**Integration 2: Product Usage DB → Data Cloud**  
→ **Purpose:** Feature usage, login frequency, seat utilization  
→ **Method:** MuleSoft API integration or Heroku Connect  
→ **Frequency:** Batch nightly, real-time for critical events

**Integration 3: Data Cloud → Salesforce CRM**  
→ **Purpose:** Real-time segment updates, calculated insights  
→ **Method:** Data Cloud Activation (native)  
→ **Frequency:** Real-time streaming

**Integration 4: Support System → Data Cloud** (Optional)  
→ **Purpose:** Support ticket volume, satisfaction scores  
→ **Method:** REST API batch import  
→ **Frequency:** Daily batch

### Data Cloud Setup:

**Data Streams:**
1. Salesforce CRM (Account, Contact, Opportunity, Asset, Campaign Member)
2. Marketing Cloud (Email Studio engagement: sends, opens, clicks, bounces)
3. Product Usage DB (feature usage, session duration, user activity logs)
4. Website Analytics (product page visits, content downloads, time on site)

**Data Model Objects:**

**Unified Individual Profile:**
- Core fields: First Name, Last Name, Email, Phone, Title, Department, Seniority
- Engagement fields: Email Opens (Last 30d), Content Downloads (Last 90d), Product Page Visits
- Product fields: Products Used, Features Accessed, Last Login Date, License Type
- Buying group fields: Role, Priority Score, Last Outreach Date

**Unified Account Profile:**
- Core fields: Account Name, Industry, Employee Count, Annual Revenue
- Product fields: Products Owned, Contract Value, Renewal Date, Implementation Date
- Health fields: Account Health Score, NPS Score, Support Ticket Volume
- Expansion fields: Expansion Opportunity Score, Buying Groups Engaged Count

**Calculated Insights:**

1. **Expansion_Propensity_Score** (Number 0-100)  
   Formula: (Product_Usage_Score × 0.4) + (Engagement_Score × 0.3) + (Account_Health × 0.2) + (Buying_Group_Coverage × 0.1)

2. **Buying_Group_Coverage** (Percentage)  
   Formula: (Unique Buying Group Roles Engaged / 5 Target Roles) × 100

3. **Engagement_Velocity** (Trend)  
   Formula: Change in engagement score over last 30 days vs. previous 30 days

**Segments (5 core + variations):**
- Economic Buyer - Expansion (criteria defined in section 3)
- Technical Evaluator - Expansion
- End User - Expansion
- Executive Sponsor - Expansion
- Influencer - Expansion

Plus segment variations:
- High Priority Expansion (Expansion_Propensity_Score > 70)
- Renewal Window (Renewal_Date within 90 days)
- Low Engagement Recovery (No engagement in 180+ days but high account health)

---

## 6. HUMAN TOUCHPOINTS

**Review Point 1: Daily Agent Draft Review (Account Owners)**  
→ **Who:** Account owners review agent-drafted emails  
→ **When:** Daily review queue (morning routine)  
→ **What:** Approve, edit, or reject drafts; adjust tone if needed  
→ **Tool:** Task queue in Salesforce (list view filter)  
→ **SLA:** <24 hours from draft creation

**Review Point 2: Weekly Messaging Framework Updates (Marketing)**  
→ **Who:** Marketing reviews new messaging, case studies added to RAG  
→ **When:** Weekly content review meeting  
→ **What:** Approve new messaging, update value props, refresh case studies  
→ **Tool:** Shared document + Data Cloud Knowledge update  
→ **Process:** Marketing submits updates → RevOps deploys to Data Cloud

**Review Point 3: Monthly Strategic Account Review (Sales Leadership)**  
→ **Who:** VP Sales, Account Directors, RevOps  
→ **When:** Monthly business review  
→ **What:** Review expansion pipeline, approve target accounts for next month, adjust buying group priorities  
→ **Tool:** Tableau/Salesforce dashboard  
→ **Decisions:** Budget allocation, resource assignment, program optimization

**Review Point 4: Quarterly Program Optimization (Cross-Functional)**  
→ **Who:** Sales, Marketing, Customer Success, RevOps  
→ **When:** Quarterly planning  
→ **What:** Review program metrics, optimize segment criteria, refine messaging, plan expansion plays  
→ **Outcomes:** Updated playbooks, revised targets, budget reallocation

---

## 7. SUCCESS DASHBOARD

### Dashboard: "Account Expansion Performance"

**Primary KPIs (Top Row):**
- **Expansion Pipeline Generated:** Target $500K/quarter | Current: [Live metric]
- **Response Rate by Buying Group:** Target 30%+ | Current: 34% (above target)
- **Meetings Booked:** Target 20+/month | Current: [Live metric]
- **Average Buying Groups Engaged per Account:** Target 3+ | Current: 3.2

**Agent Performance (Second Row):**
- **Agent Drafts Generated:** [Volume] drafts/week
- **Agent Drafts Approved %:** Target 80%+ | Current: [Live metric]
- **Time from Segment Entry → Outreach:** Target <24h | Current: [Live metric]
- **Draft Edit Rate:** % of drafts edited before approval

**Segment Health (Third Row - Bar Chart):**
- Contacts by Buying Group (Economic Buyer: 800, Technical: 1200, End User: 1500, Executive: 400, Influencer: 600)
- Engagement Rate by Buying Group (% responding)
- Top Performing Segments (which buying groups converting best)

**Account Progress (Fourth Row - Funnel):**
- Stage 1: Identified (200 accounts)
- Stage 2: 1-2 Buying Groups Engaged (120 accounts)
- Stage 3: 3+ Buying Groups Engaged (60 accounts)
- Stage 4: Expansion Opportunity Created (30 accounts)
- Stage 5: Closed-Won (15 accounts)

**Trend Analysis (Bottom Row - Line Chart):**
- Pipeline created by week (last 12 weeks)
- Response rate trend by month
- Agent draft volume and approval rate over time

### Reports to Build:
1. **Expansion Pipeline by Account** (Opportunity report grouped by Account)
2. **Buying Group Engagement Matrix** (Account × Buying Group coverage heatmap)
3. **Agent Draft Queue** (Task report for account owners)
4. **Top Performing Accounts** (Accounts with highest expansion potential)
5. **Messaging Effectiveness** (Response rate by message template/theme)

---

## 8. IMPLEMENTATION TIMELINE

**Week 1-2: Data Foundation**  
**Tasks:**
- Set up Data Cloud data streams (CRM, Marketing, Product Usage)
- Configure data model objects (Unified Individual, Unified Account)
- Build calculated insights (Expansion_Propensity_Score, Buying_Group_Coverage)
- Test data quality and completeness

**Deliverables:** Data Cloud configured with all data sources flowing

---

**Week 3: Segment Creation**  
**Tasks:**
- Create 5 buying group segments with expansion criteria
- Test segment population and quality
- Validate segment logic with sales team sample accounts
- Set up segment activation to Salesforce

**Deliverables:** 5 segments active and populating contacts, documented criteria

---

**Week 4: Messaging Framework Development**  
**Tasks:**
- Document expansion-specific pain points by persona
- Create cross-sell/upsell value propositions
- Compile customer success stories and ROI models
- Structure content for RAG (Knowledge in Data Cloud)
- Get sales/marketing approval on messaging

**Deliverables:** 38-page messaging framework stored in Data Cloud Knowledge

---

**Week 5: Agentforce Agent Build**  
**Tasks:**
- Configure Agentforce agent with instructions and actions
- Integrate RAG (connect to Data Cloud Knowledge)
- Set up account context retrieval logic
- Build agent testing environment
- Test with 10 sample contacts from each buying group

**Deliverables:** Agentforce agent operational and tested

---

**Week 6: Salesforce Configuration & Testing**  
**Tasks:**
- Create custom objects (Buying_Group__c, Agent_Draft__c, Account_Expansion_Signal__c)
- Build flows (segment trigger, draft approval, engagement threshold)
- Configure dashboard and reports
- Create task views for account owners
- End-to-end testing with pilot accounts

**Deliverables:** Full system integrated and tested

---

**Week 7: Enablement & Pilot Launch**  
**Tasks:**
- Train account owners on draft review process
- Document playbooks and FAQs
- Launch pilot with 10 strategic accounts
- Monitor daily, troubleshoot issues
- Gather feedback from account owners

**Deliverables:** Pilot live with 10 accounts, documented learnings

---

**Week 8+: Scale & Optimize**  
**Tasks:**
- Roll out to 50 accounts (Week 8)
- Roll out to all 200 accounts (Week 10)
- Monitor KPIs and optimize
- Weekly review of response rates and adjust messaging
- Monthly program review and optimization

**Deliverables:** Full program at scale, continuous improvement process

**Total Timeline:** 8 weeks to pilot, 10 weeks to full scale

---

## 9. REUSABLE COMPONENTS FROM LIBRARY

**From universal-components:**
- [X] `Buying_Group__c` custom object schema → Reuse 100%
- [X] `Agent_Draft__c` custom object schema → Reuse 100%
- [X] Segment-to-Task flow template → Adapt trigger criteria
- [X] Program performance dashboard → Customize KPIs

**From adaptable-components:**
- [X] Unified Individual profile template → Add product usage fields
- [X] Unified Account profile template → Add contract/renewal fields
- [X] Segment criteria patterns → Adapt for expansion context
- [X] Agent configuration template → Customize RAG source and context logic

**New/Program-Specific Components:**
- `Account_Expansion_Signal__c` custom object
- Expansion-specific messaging framework (38 pages)
- Account context retrieval logic in agent
- Renewal window segment

---

## 10. NOTES & DECISIONS

### Technical Decisions:

**Why Data Cloud vs. Native Segments:**
Data Cloud chosen for ability to unify product usage data with CRM and calculate real-time propensity scores. Native Salesforce segments can't access external data sources efficiently.

**Why RAG vs. Static Prompts:**
38-page messaging framework is too large for static prompts. RAG allows agent to dynamically retrieve relevant messaging based on persona, industry, and context without hitting token limits.

**Why Human-in-the-Loop:**
Expansion outreach to existing customers requires account owner context (relationship nuances, pending deals, account politics). Full automation risks poor timing or tone-deaf messaging.

### Program Decisions:

**Why 5 Buying Groups:**
Research shows enterprise decisions involve 5-7 stakeholders. Five buying groups cover 95% of decision-makers while remaining manageable.

**Why 3+ Engagement Threshold:**
Data shows accounts with 3+ buying groups engaged have 5x higher close rate than single-threaded opportunities. This threshold balances quality and volume.

### Risks & Mitigations:

**Risk:** Account owners don't review drafts promptly (bottleneck)  
**Mitigation:** SLA tracking, escalation to managers, gamification (leaderboard)

**Risk:** Data quality issues (bad email, wrong titles)  
**Mitigation:** Data validation rules, monthly data hygiene sprints, feedback loop from account owners

**Risk:** Message fatigue (contacts receiving too many emails)  
**Mitigation:** Frequency caps (max 1 email per contact per 14 days), suppression lists, engagement-based throttling

---

**Blueprint Completed By:** Michelle Bastelier, Agentforce Specialist  
**Date:** January 2025  
**Next Step:** Begin Data Cloud setup (Week 1)  
**Estimated ROI:** $500K pipeline per quarter, 30%+ response rate, 3+ buying groups engaged per account

---

**Questions or feedback on this implementation?**  
Contact: michelle@agentpilot.us
