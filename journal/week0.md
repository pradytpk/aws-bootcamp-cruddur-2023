- [Week-0 Billing and Architecture](#week-0-billing-and-architecture)
  - [Task List of 12/02/2023 to 18/02/2023](#task-list-of-12022023-to-18022023)
    - [Conceptual and Napkin Diagram](#conceptual-and-napkin-diagram)
      - [Napkin Design](#napkin-design)
      - [Conceptual Design](#conceptual-design)
    - [Logical Architectual Diagram](#logical-architectual-diagram)
    - [Weekly Outcome](#weekly-outcome)
  - [Business Scenario](#business-scenario)
  - [Architecture](#architecture)
    - [Notes](#notes)
    - [Notes Architecture](#notes-architecture)
      - [Tech Stacks](#tech-stacks)
      - [Application Layer](#application-layer)
      - [Iron triangle Management](#iron-triangle-management)


# Week-0 Billing and Architecture

## Task List of 12/02/2023 to 18/02/2023
- [x] Week 0 - Live Streamed Video(13/02/2023)
- [ ] Chirag's Week 0 - Spend Considerations
- [ ] Ashish's Week 0 - Security Considerations
- [x] Recreate Conceptual Diagram in Lucid Charts or on a Napkin (13/02/2023)
- [x] Logical Architectual Diagram in Lucid Charts (13/02/2023)
- [ ] Create an Admin User
- [ ] Use CloudShell
- [ ] Generate AWS Credentials
- [ ] Installed AWS CLI
- [ ] Create a Billing Alarm
- [ ] Create a Budget
### Conceptual and Napkin Diagram
#### Napkin Design

 <img src="../_docs/assets/napkin_design.jpg" alt="Napkin_design" width="500" height="500">

#### Conceptual Design
![Conceptual Diagram](../_docs/assets/conceptual_diagram.png)

### Logical Architectual Diagram


### Weekly Outcome
- Gain confidence when working meter-billing with a Cloud Service Provider (CSP)
- To understand how to build useful architecture diagrams
- To gain a general idea of the cost of common cloud services
- To ensure we have a working AWS account

## Business Scenario
Your company has asked to put together a technical presentation on the proposed architecture that will be implemented so it can be reviewed by the fractional CTO.
Your presentation must include a technical architectural diagram and breakdown of possible services used along with their justification.
The company also wants to generally know what spend we expect to encounter and how we will ensure we keep our spending low.

## Architecture

### Notes

Ephemeral-First Micro-blogging platform
Fractional CTO
Partly development App-keep or rebuild?
How to monetize the platform
frontend=javascript using react
backend Application = python using flask
api only
be careful with the budget
monolith into micorservice
user content(upload?)
Users-College students,Younger Students,professionals
    User Validation?
    Age limit?
Aws 
    What services?
    Set up budget monitoring
User Engagement
technical report due for investors
    Architecture
    Budget
    ongoing cost Estimate

Why User Personas?

| Personas      |                         Lessons Learned                          |
| ------------- | :--------------------------------------------------------------: |
| Tony CTO      |                   not all context is relevant                    |
| Web dev group |                        no true greenfield                        |
| Investors     |                      manage time and effort                      |
| Investors     | - Trade offs for all projects <br> - Learn iterate and show back |

### Notes Architecture

Meets the Good Requirements:

Requirements must be 
 - verifiable 
 - monitorable
 - traceable
 - feasible
  
Examples
  - Meets ISO Standards
  - 99.9% uptime
  - User can do specific task
  
Addresses the Risks,Assumptions & Constraints
- Risks can prevent the project from being successfull
  - SPoFs
  - User Commitment
  - Late Delivery
- Assumptions are factors held as true for the planning & implementations phases
  - sufficient network bandwidth
  - stake holders
  - budget is approved
- Constraints are policy or technical limitations for the projects
  - Time
  - Budget
  - Vendor Selection

From gathering the RRACs 

Conceptual Design
- Created by business stakeholders and architects
- organizers and define concept and rules
- Napkin Design

logical Desgin
- Defines the system 
- Environemt without actual names or size

Physical Design
- Representation of the actual thing that was built
- Ip Address name

Its Important to Develop a Common Dictionary 
- Ask dumb questions
- play be the packet
- Document Everything

TOGAF
- The most populat framework for EA
- Common dictory for words convey desired outcomes
- Meta-model for the creation of underlying projects
- Maps closely to the well-architected tool

The 6 pillars of AWS well architected tools are
1. Operational Excellence
2. Security
3. Relability
4. Performance Efficency 
5. Cost Optimization
6. Sustainability

#### Tech Stacks
Aws Account
ORM
Functional Requirement
Monolithic Architecture(is all one in application) into Microservice Architecture(sepearte)
AWS lambda
Budgets is fixed(Infrasturture should be based on that)

#### Application Layer

![Application_layers](../_docs/assets/application_layer.png)

#### Iron triangle Management

![iron_traingle_management](../_docs/assets/iron_triangle_management.png)
