# [PROGRAM NAME] - Salesforce Agentforce Blueprint

> **Time to complete:** 30-60 minutes  
> **Output:** Complete technical architecture ready for implementation

---

## 1. GROWTH PROGRAM OVERVIEW (5 min)

- **Program Type:** [ABM Expansion / ABM New Logo / Event / Referral / Developer / Partner]
- **Business Objective:** [Specific revenue or efficiency goal]
- **Target Audience:** [Who you're engaging - be specific with numbers]
- **Success Metrics:** 
  - Primary: [Response rate, pipeline, meetings]
  - Secondary: [Efficiency gains, time savings]
  - Tertiary: [Quality metrics, multi-threading]

---

## 2. BUYER/USER JOURNEY (10 min)

**Stage 1:** [Stage Name]  
→ **Trigger:** [What causes someone to enter this stage]  
→ **Action:** [What the agent/system does]

**Stage 2:** [Stage Name]  
→ **Trigger:** [What causes progression]  
→ **Action:** [What the agent/system does]

**Stage 3:** [Stage Name]  
→ **Trigger:** [What causes progression]  
→ **Action:** [What the agent/system does]

**Stage 4:** [Stage Name - Optional]  
→ **Trigger:** [Final conversion trigger]  
→ **Action:** [What happens]

---

## 3. DATA REQUIREMENTS (5 min)

### Data Sources:
- [ ] **CRM** - Salesforce objects: [List specific objects]
- [ ] **Marketing Automation** - [Specific data: engagement, nurture status]
- [ ] **Product Usage** - [What usage data is needed]
- [ ] **Intent Signals** - [Website, content, search activity]
- [ ] **Other** - [Firmographics, technographics, etc.]

### Contextual Data Needed:
*What context does the agent need to personalize?*
- Account context: [Current products, contract value, etc.]
- Contact context: [Role, engagement history, etc.]
- Industry context: [Pain points, use cases, etc.]

### Data Cloud Segments Needed:

1. **Segment Name:** [e.g., Economic Buyer - Expansion]  
   **Criteria:** [VP+ title, Budget authority, NOT currently engaged]  
   **Size:** [Estimated number of contacts]

2. **Segment Name:** [e.g., Technical Evaluator]  
   **Criteria:** [Engineering/IT titles, Technical decision-maker]  
   **Size:** [Estimated]

*Add 3-5 segments based on your buying groups*

---

## 4. AGENTFORCE AGENT DESIGN (5 min)

**Agent Name:** [Descriptive name - e.g., "Account Expansion Outreach Agent"]

**Agent Purpose:** [One-sentence description of what the agent does]

### Agent Actions:

1. **Action:** [Pull contact data]  
   **From:** [Data Cloud segment X]  
   **Output:** [What data is retrieved]

2. **Action:** [Generate personalized content]  
   **Using:** [RAG from messaging framework + context]  
   **Output:** [3-4 sentence email]

3. **Action:** [Create task for human]  
   **To:** [Account owner / SDR / AE]  
   **Output:** [Draft for review]

4. **Action:** [Log activity]  
   **To:** [CRM objects - Campaign, Task, etc.]  
   **Output:** [Activity record]

### Unique Context Agent Uses:
*What makes this agent's personalization powerful?*
- Example: "Your team is already using [Product X]..."
- Example: "I noticed you recently [visited pricing page]..."

### Knowledge/RAG Requirements:

**Messaging Framework Components:**
- Pain points by persona (documented how?)
- Value propositions by role
- Industry-specific use cases
- CTAs by buyer stage
- Objection handling

**Supporting Content:**
- Case studies library
- Product documentation
- Competitive differentiation
- ROI/business case templates

---

## 5. SALESFORCE ARCHITECTURE (5 min)

### Objects Used:

**Standard Objects:**
- Account, Contact, Lead, Opportunity, Campaign, Task
- [Add others specific to your program]

**Custom Objects:**
- `Buying_Group__c` (junction: Account + Contact + Role)
- `Agent_Draft__c` (stores agent-generated content)
- [Add program-specific objects]

### Key Fields Added:

**Account Fields:**
- [e.g., Expansion_Opportunity_Score__c]
- [e.g., Engaged_Buying_Groups_Count__c]

**Contact/Lead Fields:**
- [e.g., Buying_Group_Role__c]
- [e.g., Cold_Outreach_Priority__c]

### Flows/Automation:

**Flow 1:** [Name]  
→ **Trigger:** [Event that starts the flow]  
→ **Action:** [What the flow does]

**Flow 2:** [Name]  
→ **Trigger:** [Event]  
→ **Action:** [What happens]

### Integrations:

1. **Integration:** [Marketing Cloud → Data Cloud]  
   **Purpose:** [Email engagement data]  
   **Method:** [Native connector / Mulesoft / API]

2. **Integration:** [Intent Data Provider → Data Cloud]  
   **Purpose:** [Website visits, content consumption]  
   **Method:** [API / Batch]

### Data Cloud Setup:

**Data Streams:**
- Salesforce CRM (Account, Contact, Opportunity)
- [Marketing automation platform]
- [Product usage database]
- [Intent data provider]

**Data Model Objects:**
- Unified Individual (Contact + engagement + intent)
- Unified Account (Company + context + signals)

**Calculated Insights:**
- [e.g., Expansion_Propensity_Score]
- [e.g., Buying_Group_Coverage_%]

**Segments:** [Reference section 3 - your 3-5 segments]

---

## 6. HUMAN TOUCHPOINTS

**Review Point 1:** [Who reviews what, when]  
Example: Account owner reviews agent-drafted emails daily

**Review Point 2:** [Who reviews what, when]  
Example: Marketing reviews new messaging weekly

**Review Point 3:** [Who reviews what, when]  
Example: Sales leadership approves target accounts monthly

---

## 7. SUCCESS DASHBOARD

### Key Metrics:

**Primary KPIs:**
- [Metric 1]: Target [X]
- [Metric 2]: Target [Y]
- [Metric 3]: Target [Z]

**Agent Performance:**
- Agent drafts generated: [Volume]
- Agent drafts approved: [%]
- Time to [action]: [Duration]

**Program Health:**
- Segment size by buying group
- Engagement by persona
- Pipeline velocity
- Multi-threading % (if applicable)

### Dashboard Components:
- [List the charts/visualizations you need]

---

## 8. IMPLEMENTATION TIMELINE

**Week 1-2:** [Phase 1 - Data Foundation]  
Tasks: Data Cloud setup, data streams, unified profiles

**Week 3-4:** [Phase 2 - Segmentation]  
Tasks: Segment creation, criteria testing, quality check

**Week 5:** [Phase 3 - Messaging Framework]  
Tasks: RAG content development, persona messaging

**Week 6:** [Phase 4 - Agent Build]  
Tasks: Agentforce configuration, RAG integration, testing

**Week 7:** [Phase 5 - Pilot]  
Tasks: Deploy to [X] pilot accounts, monitor, optimize

**Week 8+:** [Phase 6 - Scale]  
Tasks: Roll out to all accounts, continuous improvement

**Total Timeline:** [6-8 weeks typical]

---

## 9. REUSABLE COMPONENTS FROM LIBRARY

*Which components from the library can you reuse?*

**From universal-components:**
- [ ] Buying_Group__c object
- [ ] Agent_Draft__c object
- [ ] Segment_to_Task flow
- [ ] Program performance dashboard

**From adaptable-components:**
- [ ] Unified profile template (customize fields)
- [ ] Segment criteria patterns (adjust logic)
- [ ] Agent configuration template (change RAG source)

**From program-implementations:**
- [ ] [Similar program] messaging framework (adapt)
- [ ] [Similar program] segment definitions (reference)

---

## 10. NOTES & DECISIONS

*Document key decisions, trade-offs, and lessons learned*

**Technical Decisions:**
- [Why we chose X over Y]

**Program Decisions:**
- [Why we structured the journey this way]

**Risks & Mitigations:**
- [Potential issue → How we're handling it]

---

**Blueprint completed by:** [Your name]  
**Date:** [Date]  
**Next step:** [Typically: Begin Data Cloud setup]
