# CrowdWire - Massive Online Meetings

This repository aims to describe the Project Planning, Architecture and Documentation for the CrowdWire Project.

[TOC]

## Inception Phase

### Context

With the emergence of Covid-19 all around the World, many people,  companies and organizations started adopting remote procedures like  video-conferences to continue doing the commons tasks they used to do  "in person". Therefore, the search and use of these types of systems  that allow video and voice calls has increased a lot.

## 

### Problem

Most of the current video communication systems are limited in the  sense that they do not provide a remote interactive environment, side  conversations, nor visualization that mimics real life behaviours. To  solve this issue we want to incorporate, as much as possible, this  component which is one of the most rewarding thing in real life  meetings. Besides this, the ones that do, are not open source projects.

## 

### Goals

With this work, we aim to provide an interactive way of doing virtual meetings, online conferences and classes, capable of scaling up to a   number of active users, that should be close enough to host conferences. Also, we want to simulate a real-life communication experience by taking into consideration users' proximity. In order to do so, we are looking forward to develop a web application  with a game-like interface that allows to create and customize  environments and invite other users. As a solution to part of the problem, we intend to do a open-source  project, so that people are able to use and contribute to it.

## 

### Tasks

Module Backend (Bruno Bastos, Mário Silva, Daniel Gomes)

- Task 1: Identify the databases that will be used according to its use cases (Bruno Bastos)
- Task 2: Create the database schema (Bruno Bastos,Mário Silva)
- Task 3: Develop the API  and its endpoints (Daniel Gomes, Bruno Bastos)
- Task 4: Integrate with the Communications logic (Bruno Bastos, Mário Silva)

Module Frontend (Leandro Silva, Pedro Tavares)

- Task 1: Provide a static interface with an embedded game framework (Leandro Silva, Pedro Tavares)
- Task 2: Create the required communication services with the backend (Leandro Silva, Pedro Tavares)
- Task 3: Create dynamic pages and present information in real time where needed (Leandro Silva, Pedro Tavares)

Module Communications (Mário Silva, Daniel Gomes)

- Task 1: Investigate WebRTC technology to perform video and voice calls (Mário Silva)
- Task 2: Create the communications  Service (Mário Silva)
- Task 3: Integrate this microservice with the backend and frontend (Mário Silva, Daniel Gomes)

Module Infrastructure (Daniel Gomes, Mário Silva)

- Task 1: Identify the technologies that are needed to deploy every micro-service (Daniel Gomes)
- Task 2: Investigate how to increase the communications service availability in the production environment (Daniel Gomes)
- Task 3: CI Pipeline (Daniel Gomes, Mário Silva)
- Task 4: CD Pipeline (Daniel Gomes)

Module World-Editor (Leandro Silva, Pedro Tavares)

- Task 1: Provide the user with a map editor and material to create and edit its personal world (Leandro Silva, Pedro Tavares)
- Task 2: Allow users to upload sprites to their editor (Leandro Silva)

## 

## Expected Results

In the final result, we expect to have a fully functional web  application capable of performing video and voice calls that may be used in many different ways, providing to the end users other kind of  interaction with each other.

The end application should allow the user to create and edit their  own worlds and invite friends, co-workers or guests depending on the  world's intent, which can go from speeches to workplaces, conferences,  classes or maybe even playgrounds.

Finally, this platform should  be scalable enough to host video-conferences with dimensions of an event like Students@Deti.

## 

## Related Work

The following system is really interesting and inspiring in the context of our project:

- [**Gather.town**](https://gather.town/)
- [**DogeHouse**](https://dogehouse.tv/)

## 

### Calendar

#### 1st Milestone

- Set up docs platforms tools
- Develop a prototype
- Research technologies and define the system architecture
- Start testing and developing shortly each area/framework individually

#### 2nd Milestone

- Basic User movement on predefined maps
- Video and voice communication
- Text Chat feature
- Backend Structure and databases
- User Interface

### 3rd Milestone

- World-Editor
- Full Integration of each micro-service
- Proximity video and voice chatting with high availability
- CI/CD
- File Exchange feature

### 4th Milestone

- Map and User Permissions well integrated
- Stress Testing to all features
- Integrate additional features

## 

### Communication

Backlog Management: For backlog management we decided to use Jira  since it is a widely used tool by a lot of Companies as a project  Management tool that allows bug/issue tracking. Git Platform: For the Git platform, we have chosen GitHub since we are  very acquainted with it. Git Standards:

- For each new feature create a new branch.
- For each fix create a new branch.
- Never merge directly, always make pull requests and identify at  least one person to check (review) that pull request before merging the  PR.
- New feature branch: For each new feature create a branch following the standard, example: feature-frontend-feature-name.
- New Issue branch: For each fix create a branch following the standard, example: hotfix-frontend-fix-name.
- Follow the Good Practices stablished for most of the Open Source Projects.
- Always have instructions for running all services on local host.
- For each pull request it's assigned a member to revise the code and  merge it, we decided to use a Round Robin policy for the assignment of  the reviewer.

Team Communication: For intra-team communication we are using  Discord, since every member is familiarized with the tool and, we have  integrated it with Jira and GitHub for continuous updates on our  repository.

## 

### Team Roles

- **Product Owner**: Leandro Silva 
- **DevOps Master**: Daniel Gomes 
- **Architect**: Bruno Bastos
- **Lead Developer**: Mário Silva 
- **Project Manager**: Pedro Tavares 
- **Advisor**: Diogo Gomes