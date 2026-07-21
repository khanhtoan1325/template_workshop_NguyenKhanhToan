---
title: "Event 2"
date: 2026-06-27
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Reflection Report: “Cloud, AI Agent, and Amazon Q on AWS”

### Purpose of the Event

- To share practical knowledge about Cloud Computing, AI Agents, DevOps AI, and system security on AWS.
- To introduce applications of Generative AI in enterprises, such as voice assistants, DevOps automation, and human resource management.
- To present how AWS services such as Amazon Bedrock, Amazon Q, Amazon ECS, VPC, Interface Endpoint, Route 53 Resolver, and Application Load Balancer support the development of modern AI systems.
- To help participants better understand the trend of combining Cloud, AI, and Automation in system development, operation, and security.
- To guide students and developers in developing skills that match the IT/Cloud job market in the AI era.

### List of Speakers

- **Steve Trần** – Founder of Cloud Thinker
  Topic: *Career Path with Cloud and Introduction to Cloud Thinker*

- **Hiếu Nghị** – Renova Cloud
  Topic: *Building an AI Voice Assistant*

- **Kiệt** – AWS Study Group
  Topic: *Voice Agent and AI Applications on AWS*

- **Trung Nguyễn** – Founder & CEO of R AI
  Topic: *Deploying Voice AI for the Vietnamese Language*

- **Bảo** – Cloud Kinetic
  Topic: *Introduction to AWS DevOps AI Agent*

- **Nguyên Nguyễn** – Cloud Engineer, Cloud Kinetic
  Topic: *DevOps AI Agent and Incident Handling on AWS*

- **Trường** – Solution Architect, Noventic
  Topic: *Applying Amazon Q in Human Resource Management*

- **Minh Anh** – Solution Architect, Noventic
  Topic: *Amazon Q and HR Workflow Automation*

- **Toàn Nguyễn** – AWS Security Builder
  Topic: *Securing Amazon Q with Private Connection*

### Key Highlights

#### Career Path with Cloud and Introduction to Cloud Thinker

The first session was presented by Steve Trần and focused on his career development journey in the Cloud field. He shared how he started learning Cloud, once failed an Azure certification exam, then switched to AWS, became a Solution Architect at AWS Vietnam, and eventually founded his own startup, Cloud Thinker.

The main points included:

- Learning Cloud is a long journey that requires persistence and continuous learning.
- Failing while studying or taking certification exams is not the end, but an experience that helps learners continue improving.
- AI is changing the way developers write code, operate systems, and handle daily tasks.
- AI can help speed up coding, but it cannot completely replace humans in critical systems.
- Enterprises still need engineers with strong technical foundations who know how to apply AI effectively.

In addition, the speaker introduced Cloud Thinker’s **Agentic Platform**. This platform aims to use AI Agents to support tasks such as incident handling, code review before production deployment, Cloud cost optimization through FinOps, and security testing.

Another notable point was the difference between **Single Agent** and **Multi-Agent** architecture. A Single Agent is suitable for simple tasks, while Multi-Agent architecture helps divide tasks, manage context more effectively, and optimize the operating cost of AI models.

#### Building an AI Voice Assistant

This session introduced how to build a **Voice Agent** system using AI. A typical Voice AI architecture consists of three main components: **Speech-to-Text**, **LLM**, and **Text-to-Speech**.

The basic workflow is as follows:

- The user speaks to the system.
- Speech-to-Text converts the voice input into text.
- The LLM processes the content and generates a response.
- Text-to-Speech converts the response into voice output and replies to the user.

In the demo, the Voice Agent system was used to answer questions about Apple products, specifically the MacBook Pro. The demo was deployed on AWS Bedrock infrastructure, helping participants better understand how AI can be applied in customer support, product consultation, and automated voice communication.

The main challenges when deploying Voice AI for Vietnamese included:

- Vietnamese is a lower-resource language compared to English.
- Low latency needs to be handled through real-time data streaming.
- The system needs to recognize gender in order to use appropriate forms of address such as “anh” or “chị”.
- The AI needs to understand when to interrupt and when to remain silent so that the conversation feels more natural.
- The system must handle differences in regional accents.
- There should be a mechanism to transfer the conversation to a human agent when AI cannot handle the request.

An important point in this session was the **Human-in-the-loop** model. When the AI is overloaded, gives poor responses, or the customer is not satisfied, the system can smoothly transfer the call to a human support agent. This shows that AI should be designed to cooperate with humans instead of operating completely independently.

#### Introduction to AWS DevOps AI Agent

This session focused on system operations and incident handling in a Cloud environment. In the past, when a system had issues, DevOps engineers had to manually check many data sources such as logs, metrics, dashboards, and alerts. The process of finding the root cause often took a lot of time, especially in large and distributed systems.

The **DevOps AI Agent** solution was introduced to automate the incident investigation process. This tool helps engineers quickly analyze the system status, identify possible causes, and suggest mitigation plans.

The main pillars of DevOps AI Agent include:

- **Context Learning**: learning and understanding the system context.
- **Control**: ensuring that humans still have control over final decisions.
- **Integration**: integrating with tools through MCP tools.
- **Collaboration**: supporting collaboration through Slack, ServiceNow, and other operations platforms.
- **Convenient**: making it easier for engineers to work during incident handling.
- **Cost-effective**: optimizing cost by charging based on actual runtime.

In the live demo, the speakers simulated a denial-of-service attack against an e-commerce application running on AWS ECS. When the application became severely slow, the DevOps AI Agent analyzed the data, identified the cause, and provided a mitigation plan within a few minutes.

The key lesson from this session is that an AI Agent can only work effectively when the system has **Good Observability**, meaning it must have sufficient logs, metrics, and monitoring information. AI does not replace DevOps engineers; instead, it supports them and accelerates the process of investigating and resolving incidents.

#### Applying Amazon Q in Human Resource Management

This session presented how **Amazon Q** can be applied in human resource management. HR departments often face many difficulties, such as manually screening CVs, spending time writing job descriptions, evaluating candidates based on subjective opinions, and worrying about security risks when uploading internal data to public AI tools.

Amazon Q was introduced as an enterprise AI assistant that can connect to various data sources such as SharePoint, OneDrive, Google Drive, GitHub, Jira, and Amazon S3. Through Action Connectors and MCP, Amazon Q can support data retrieval, analysis, and workflow automation based on internal enterprise data.

In the demo, Amazon Q was used to:

- Automatically draft a job description for a Junior Cloud Engineer position.
- Activate the **HR Talent Review Assistant** skill to scan a folder containing candidate CVs.
- Analyze CVs based on criteria such as technical skills and communication.
- Score and classify candidates as Pass or Reject.
- Export a visual report as an HTML file.
- Synchronize the recruitment workflow to a pipeline tracking application built with No-code/Low-code.

This session showed that AI can help HR reduce repetitive tasks, speed up the recruitment process, and make candidate evaluation more systematic. However, because HR data is sensitive, security must be a top priority when implementing such a solution.

#### Securing Amazon Q with Private Connection

The final session focused on security when connecting Amazon Q with MCP Servers or third-party systems. If data travels through the public Internet, enterprises may face many risks such as Man-in-the-middle attacks, DDoS attacks, or internal data leakage.

The proposed solution was to move the connection flow into a private VPC network using a **Private Connection** architecture. This architecture uses several AWS components to isolate the data flow from the public Internet.

The main components include:

- **VPC Connection** to connect systems within a private network environment.
- **Interface Endpoint** to access services privately.
- **Route 53 Resolver** to handle DNS resolution in the internal environment.
- **Application Load Balancer** to distribute requests.
- **TLS** to encrypt data during transmission.

In the demo, the speaker performed secure queries and checked system latency while operating through a private environment. This helped participants understand that when deploying AI in enterprises, security should not only be handled at the application layer but also at the network, connection, and data flow layers.

One point to consider is operational cost. Advanced security architecture may increase costs because of endpoints, network infrastructure, and data transfer. However, for systems that process internal data or customer data, this cost is reasonable to ensure information security.

### What I Learned

#### Technical Knowledge

- Cloud Computing remains an important foundation for deploying modern AI systems.
- AI Agents can support many tasks such as incident handling, code review, cost optimization, and security testing.
- A Voice Agent is usually built based on three main components: Speech-to-Text, LLM, and Text-to-Speech.
- When deploying Voice AI for Vietnamese, it is important to consider latency, forms of address, regional accents, and natural conversation experience.
- DevOps AI Agent can reduce incident investigation time, but it requires a system with good observability.
- Amazon Q can help enterprises automate workflows such as CV analysis, job description creation, and recruitment management.
- Private Connection helps improve security when connecting AI to internal systems or third-party MCP Servers.
- Multi-Agent Architecture is suitable for complex problems that require task division and good context management.

#### Technical Mindset

- AI should be considered a tool that supports and amplifies human capabilities, not a tool that completely replaces engineers.
- When building AI systems, it is necessary to consider performance, cost, security, and user experience at the same time.
- Production systems should be designed with good observability through logs, metrics, and monitoring.
- For internal enterprise data, it is not recommended to upload data to public AI tools without proper security controls.
- Human-in-the-loop is an important design approach to ensure service quality when AI is not capable of handling everything.
- Developers need to learn how to combine backend, cloud, AI, and security knowledge to adapt to new technology trends.

### Application to Study and Work

The knowledge gained from this event can be applied to my learning process and personal projects in the following ways:

- Study AWS more deeply, especially Amazon Bedrock, Amazon Q, ECS, VPC, and network security services.
- Apply AI Agent thinking to personal projects such as a learning-support chatbot, document search assistant, or automated log analysis system.
- Improve backend projects by adding clearer logging, monitoring, and error handling.
- When building AI applications, design workflows that allow humans to control important steps.
- Learn more about Multi-Agent architecture for complex automation problems.
- Apply security knowledge such as private networks, TLS, endpoints, and access permission control when deploying applications on Cloud.
- Practice using AI as a tool to support learning, coding, debugging, and system analysis.

### Event Experience

Participating in this event was a very useful experience for me. The content was not only theoretical but also included many practical demos, which helped me better understand how AI and AWS are applied in real enterprise environments.

I was impressed by the demos about Voice Agent, DevOps AI Agent, and Amazon Q in the HR workflow. These examples showed that AI can be applied in many different fields, from customer support and system operations to human resource management.

As a Software Engineering student with an orientation toward Backend Development, this event helped me realize that besides programming skills, I also need to learn more about Cloud, DevOps, AI Agents, security, and system architecture. These are important skills for career development in the AI era.

#### Some Photos from the Event

{{< image
  src="images/events/event2.jpg"
  alt="Cloud, AI Agent và Amazon Q trên AWS"
>}}

> Overall, the event brought me a lot of useful knowledge about Cloud, AI Agents, Amazon Q, and system security on AWS. It also gave me a clearer direction for learning and developing the skills needed to pursue Backend, Cloud, and AI in the future.