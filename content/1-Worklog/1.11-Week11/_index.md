---
title: "Week 11 Worklog"
date: "2026-07-14"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:
* Learn resource monitoring concepts using Amazon CloudWatch.
* Explore Infrastructure as Code (IaC) with AWS CloudFormation templates.
* Co-work on development and integration phases of the team project.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 3 | - **Amazon CloudWatch** <br> - Learn about CloudWatch Metrics <br> - Learn about CloudWatch Logs <br> - Learn about CloudWatch Alarms <br> - Note down monitoring best practices | 14/07/2026 | 14/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 |- **Project** <br> - Integrate Remotion Player into the video preview interface (configured canvas 1080x1920 (9:16), 30fps)<br>- Connect playerRef to Zustand store for triggerable play/pause/seekTo actions across components<br>- Integrate @designcombo/timeline: track drag-and-drop, zoom, and timeline scrolling<br>- Handle timeline events via @designcombo/events (RxJS-like pattern): PLAYER_PLAY, PLAYER_PAUSE, PLAYER_SEEK, TIMELINE_SEEK<br>- Add keyboard shortcuts: L (lock timeline), P (lock player), F (fullscreen)<br>- Integrate getVideoMetadata() to automatically compute video duration | 15/07/2026 | 15/07/2026 |<https://www.remotion.dev/> |
| 5 | - **AWS CloudFormation** <br> - Learn about Infrastructure as Code (IaC) <br> - Learn about CloudFormation Templates <br> - Note down components: Resources, Parameters, Outputs <br> - Describe advantages of infra automation | 16/07/2026 | 16/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6 |- **Project** <br> - Amazon RDS MySQL – Database Configuration for the System<br>- Create a MySQL RDS instance in the ap-southeast-2 region<br>- Configure Security Group to allow EC2 inbound connections on port 3306<br>- Create database db_sub_video, set up user accounts, and assign permissions<br>- Connect Backend (SQLAlchemy) to the RDS endpoint<br>- Configure connection pool: pool_recycle=3600, pool_pre_ping=True<br>- Verify public/private access settings and disable public access for enhanced security | 17/07/2026 | 17/07/2026 |<https://cloudjourney.awsstudygroup.com/>  |

### Week 11 Achievements:
* Configured basic CloudWatch Alarms to watch CPU usage and gathered metrics from instances.
* Examined JSON/YAML CloudFormation templates to understand structural syntax (Resources, Parameters).
* Accelerated core features of the team project to meet planned milestones.
