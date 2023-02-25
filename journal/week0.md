- [1. Week-0 Billing and Architecture](#1-week-0-billing-and-architecture)
  - [1.1. Task List of 12/02/2023 to 18/02/2023](#11-task-list-of-12022023-to-18022023)
  - [1.2. Homework Summary](#12-homework-summary)
    - [1.2.1. Conceptual and Napkin Diagram](#121-conceptual-and-napkin-diagram)
      - [1.2.1.1. Napkin Design](#1211-napkin-design)
      - [1.2.1.2. Conceptual Design](#1212-conceptual-design)
      - [1.2.1.3. Logical Architectual Diagram](#1213-logical-architectual-diagram)
      - [1.2.1.4. Physical Design](#1214-physical-design)
      - [1.2.1.5. Application Layer](#1215-application-layer)
    - [1.2.2. Install AWS CLI](#122-install-aws-cli)
    - [1.2.3. Create a new User and Generate AWS Credentials](#123-create-a-new-user-and-generate-aws-credentials)
    - [1.2.4. Set Environment Variable in gitpod](#124-set-environment-variable-in-gitpod)
    - [1.2.5. Check that the AWS CLI is working and you are the expected user](#125-check-that-the-aws-cli-is-working-and-you-are-the-expected-user)
    - [1.2.6. Enable Billing](#126-enable-billing)
    - [1.2.7. Creating a Billing Alarm](#127-creating-a-billing-alarm)
      - [1.2.7.1. Create SNS Topic](#1271-create-sns-topic)
      - [1.2.7.2. Create Alarm](#1272-create-alarm)
      - [1.2.7.3. Create an AWS Budget](#1273-create-an-aws-budget)
  - [1.3. Chirag's Week 0 - Spend Considerations](#13-chirags-week-0---spend-considerations)
      - [1.3.0.1. Aws Pricing basics and Free Tier](#1301-aws-pricing-basics-and-free-tier)
  - [1.4. Ashish's Week 0 - Security Considerations](#14-ashishs-week-0---security-considerations)
      - [1.4.0.1. CyberSecurity Goal](#1401-cybersecurity-goal)
      - [1.4.0.2. Cloud Security](#1402-cloud-security)
      - [1.4.0.3. Why care about cloud security](#1403-why-care-about-cloud-security)
      - [1.4.0.4. Why cloud security requires practice](#1404-why-cloud-security-requires-practice)
      - [1.4.0.5. Cloud Security Best Practice](#1405-cloud-security-best-practice)
      - [1.4.0.6. Security Best Practices](#1406-security-best-practices)
  - [1.5. Well Architected Tool](#15-well-architected-tool)
  - [1.6. Tech Stacks](#16-tech-stacks)
  - [1.7. Iron triangle Management](#17-iron-triangle-management)
    - [1.7.1. Notes](#171-notes)
      - [1.7.1.1. How to Take the notes of RG during the CTO/Client meeting?](#1711-how-to-take-the-notes-of-rg-during-the-ctoclient-meeting)
      - [1.7.1.2. Meets the Good Requirements:](#1712-meets-the-good-requirements)
      - [1.7.1.3. Addresses the Risks,Assumptions \& Constraints](#1713-addresses-the-risksassumptions--constraints)
      - [1.7.1.4. From gathering the RRACs](#1714-from-gathering-the-rracs)
      - [1.7.1.5. TOGAF](#1715-togaf)

# 1. Week-0 Billing and Architecture

## 1.1. Task List of 12/02/2023 to 18/02/2023
- [x] Week 0 - Live Streamed Video(13/02/2023)
- [x] Chirag's Week 0 - Spend Considerations (14/02/2023)
- [x] Ashish's Week 0 - Security Considerations (14/02/2023)
- [x] Recreate Conceptual Diagram in Lucid Charts or on a Napkin (15/02/2023)
- [x] Logical Architectual Diagram in Lucid Charts (15/02/2023)
- [x] Create an Admin User(16/02/2023)
- [x] Use CloudShell(16/02/2023)
- [x] Generate AWS Credentials(16/02/2023)
- [x] Installed AWS CLI(16/02/2023)
- [x] Create a Billing Alarm (14/02/2023)
- [x] Create a Budget (14/02/2023)
- [x] Well Architected Tool(17/02/2023)
- [x] Homework Summary (17/02/2023)


## 1.2. Homework Summary 

I was able to completed all the assignment.
I faced challenge during showing the billing console in the IAM User billing console.
I overcome  the above issue by enabling the billing console setting in root account settings

### 1.2.1. Conceptual and Napkin Diagram
- Created by business stakeholders and architects
- organizers and define concept and rules
- Napkin Design

#### 1.2.1.1. Napkin Design
 <img src="../_docs/assets/napkin_design.jpg" alt="Napkin_design" width="500" height="500">

#### 1.2.1.2. Conceptual Design
![Conceptual Diagram](../_docs/assets/conceptual_diagram.png)

#### 1.2.1.3. Logical Architectual Diagram
- Defines the system 
- Environment without actual names or size
- https://lucid.app/lucidchart/d2099518-39c3-4584-ae5c-e6afd0e54dfa/edit?viewport_loc=-472%2C-172%2C3156%2C1646%2C0_0&invitationId=inv_6dfb2cb9-f0b4-4e1b-b356-84dbada70f0d
![logical_design](../_docs/assets/logical_diagram.png)

#### 1.2.1.4. Physical Design
- Representation of the actual thing that was built
- Ip Address name
#### 1.2.1.5. Application Layer
![Application_layers](../_docs/assets/application_layer.png)

### 1.2.2. Install AWS CLI

- Install the AWS CLI when our Gitpod enviroment lanuches.
- Set AWS CLI to use partial autoprompt mode to make it easier to debug CLI commands.

Update our `.gitpod.yml` to include the following task.

```sh
tasks:
  - name: aws-cli
    env:
      AWS_CLI_AUTO_PROMPT: on-partial
    init: |
      cd /workspace
      curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      sudo ./aws/install
      cd $THEIA_WORKSPACE_ROOT
```

### 1.2.3. Create a new User and Generate AWS Credentials

- Go to (IAM Users Console](https://us-east-1.console.aws.amazon.com/iamv2/home?region=us-east-1#/users) 
- Create a new user
- `Enable console access` for the user
- Create a new `Admin` Group and apply `AdministratorAccess`
- Create the user and go find and click into the user
- Click on `Security Credentials` and `Create Access Key`
- Choose AWS CLI Access
- Download the CSV with the credentials

### 1.2.4. Set Environment Variable in gitpod

Set these credentials for the current bash terminal
```
export AWS_ACCESS_KEY_ID="XXXXX"
export AWS_SECRET_ACCESS_KEY="XXXXX"
export AWS_DEFAULT_REGION="XXXXX"
```
Tell Gitpod to remember these credentials if we relaunch our workspaces
```
gp env AWS_ACCESS_KEY_ID="XXXXX"
gp env AWS_SECRET_ACCESS_KEY="XXXXX"
gp env AWS_DEFAULT_REGION="XXXXX"
```

### 1.2.5. Check that the AWS CLI is working and you are the expected user

```sh
aws sts get-caller-identity
```

You should see something like this:
```json
{
    "UserId": "XXXX",
    "Account": "XXXX",
    "Arn": "XXXXX"
}
```

### 1.2.6. Enable Billing 

- In your Root Account go to the [Billing Page](https://console.aws.amazon.com/billing/)
- Under `Billing Preferences` Choose `Receive Billing Alerts`
- Save Preferences

### 1.2.7. Creating a Billing Alarm

#### 1.2.7.1. Create SNS Topic

We'll create a SNS Topic
```sh
aws sns create-topic --name DailyEstimatedCharges
```
![sns](../_docs/assets/sns.png)
```sh
aws sns subscribe \
    --topic-arn TopicARN \
    --protocol email \
    --notification-endpoint your@email.com
```

Check your email and confirm the subscription
![confirmation](../_docs/assets/mailconfirm.png)
#### 1.2.7.2. Create Alarm

```sh
aws cloudwatch put-metric-alarm --cli-input-json file://aws/json/alarm_config.json
```
![alarm](../_docs/assets/alarm.png)
#### 1.2.7.3. Create an AWS Budget

```sh
aws sts get-caller-identity --query Account --output text
```
```sh
aws budgets create-budget \
    --account-id AccountID \
    --budget file://aws/json/budget.json \
    --notifications-with-subscribers file://aws/json/budget-notifications-with-subscribers.jsons
```
![budget](../_docs/assets/budget.png)

##  1.3. Chirag's Week 0 - Spend Considerations
#### 1.3.0.1. Aws Pricing basics and Free Tier
- AWS Bill
  - Pricing Varies depends on the region
  - Created a budgets(2 budgets for free in free tier)
- Billing Alert
  - Created a Bill alerts for the free tier account
  - Created a alarm for the boot camp
  - 10 alarm  are free for the free tier
- Cost Explorer
  - Calculate AWS estimates Cost for service
    - I have checked the ec2 instance cost for 1 month using aws calculator
  - Check AWS allocation tags
  - Cost allocation tags is a key value pair
  - Free forever vs Free for 12 months
    - https://aws.amazon.com/free/
  
##  1.4. Ashish's Week 0 - Security Considerations
#### 1.4.0.1. CyberSecurity Goal
  - Identify & inform the business on any technical risk that the business maybe exposed to.
#### 1.4.0.2. Cloud Security
  - Cyber security that protects the data, application and services assocaited wih cloud environments form both external and interna security threats
#### 1.4.0.3. Why care about cloud security
- Reducing impact of breach
- Protecting
- Reducing the human error
#### 1.4.0.4. Why cloud security requires practice
- Complexity
- Always chasing out tail with new service
- Bad hackers are improving their game
#### 1.4.0.5. Cloud Security Best Practice
- Enable MFA
- Create an Organization unit
- Enable AWS Cloud Trail
- Create IAM User
  - Tips
    - Enable MFA
    - Principle of Least Privilege
  - Create IAM roles using Custom purpose
  - Create Group
  - Create Roles
  - Create policies
- Security Control Policies
- Shared Responsibility Models

#### 1.4.0.6. Security Best Practices
- Data Protection & Residency in accordance to Security Policy
- IAM with Least Privilege
- Governance & Compliance of AWS Services being used 
  - Global vs Regional Services
  - Compliant Services
- Shared Responsibility of Threat Detection
- Inicident Response Plans to include Cloud

## 1.5. Well Architected Tool
The 6 pillars of AWS well architected tools are
1. Operational Excellence
2. Security
3. Relability
4. Performance Efficency 
5. Cost Optimization
6. Sustainability

## 1.6. Tech Stacks
- React
- Python

## 1.7. Iron triangle Management

![iron_traingle_management](../_docs/assets/iron_triangle_management.png)

### 1.7.1. Notes
#### 1.7.1.1. How to Take the notes of RG during the CTO/Client meeting?
- Ephemeral-First Micro-blogging platform
- Fractional CTO
- Partly development App-keep or rebuild?
- How to monetize the platform
- frontend=javascript using react
- backend Application = python using flask
- api only
- be careful with the budget
- monolith into micorservice
- user content(upload?)
- Users-College students,Younger Students,professionals
  - User Validation?
  - Age limit?
- AWS 
  - What services?
  - Set up budget monitoring
- User Engagement
- Technical report due for investors
  - Architecture
  - Budget
  - ongoing cost Estimate

Why User Personas?

| Personas      |                         Lessons Learned                          |
| ------------- | :--------------------------------------------------------------: |
| Tony CTO      |                   not all context is relevant                    |
| Web dev group |                        no true greenfield                        |
| Investors     |                      manage time and effort                      |
| Investors     | - Trade offs for all projects <br> - Learn iterate and show back |

#### 1.7.1.2. Meets the Good Requirements:

Requirements must be 
 - verifiable 
 - monitorable
 - traceable
 - feasible
  
Examples
  - Meets ISO Standards
  - 99.9% uptime
  - User can do specific task
  
#### 1.7.1.3. Addresses the Risks,Assumptions & Constraints
- Risks can prevent the project from being successfull
  - SPOFs
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

#### 1.7.1.4. From gathering the RRACs 

Its Important to Develop a Common Dictionary 
- Ask dumb questions
- play be the packet
- Document Everything

#### 1.7.1.5. TOGAF
- The most populat framework for EA
- Common dictory for words convey desired outcomes
- Meta-model for the creation of underlying projects
- Maps closely to the well-architected tool