---
title: "About"
layout: single
permalink: /about/
author_profile: true
sidebar_main: true
---
# Roger Kim

Welcome! I am Roger Kim, a computer science student at Hanyang University in Seoul, South Korea. With expertise in Python and experience in C, C++, and C#, I am now aiming to work as a freelance web developer, using Django as my framework. Additionally, I have a thorough understanding of networking fundamentals and is proficient in various DevOps tools, such as Docker, AWS ECS, Git, and GitHub.

## My key skills
- Back-end development with ***django***
- REST API with ***DRF(Django Rest Framework)***
- Containerization with ***docker***
- Data Manipulation with ***python***
- Deploying with various ***AWS*** tools(Elastic Containers, RDS, VPC, etc.)
- Designing Software

## Projects
## Web-application(Backend) - TOYKI (Developing)
<p float="left">
  <img src="/assets/img/toyki-homepage.png" width="100%" />
</p>

[TOYKI](https://toyki-homepage.vercel.app/) is a service that provides opportunities to overcome the limitations of offline human relationships and enables everyone to build social networks more easily. It is currently under development, and I am developing Backend API. Learn more about [TOYKI](https://toyki-homepage.vercel.app/) here:

https://toyki-homepage.vercel.app/


**Tech Stack**
- React
- **DRF** for REST API
- **Docker** for containerization
- **ECS** for deployment
- **PostgreSQL** with **RDS** for DB

## Web-application(Full) - cmpnyinfo
<p float="left">
  <img src="/assets/img/cmpnyinfo_portfolio_detail_eng.png" width="45%" />
  <img src="/assets/img/cmpnyinfo_portfolio_main.png" width="44%" /> 
</p>
This is a simple website that analyses the financial statements of corporations registered in Korean Composite Stock Price Indexes(KOSPI). It provides ***essential analytical data*** and ***visual representation*** using variouse types of graphs.

**Tech Stack**
- pure html&css for front
- **django** for back
- **Docker** for containerization
- **ECS** for deployment

## OpenSource - NAVER Shopping Insight
<p float="left">
  <img src="/assets/img/naver1.png" width="95%" />
  <img src="/assets/img/naver2.png" width="95%" />
</p>
A opensource project. Visit it [here](https://github.com/RogerKimJazzLover/NAVER_shopping_insight). 
This is an API-based application that gathers information such as, 
1. the most searched keywords for shopping categories, from one of South Korea's biggest IT company, NAVER.
2. other such as monthly searched numbers, product numbers, competition index, etc.

**⚙️ Languages and Packages Used**
- Language use: python
- Packages used: **`pandas`**, and more.

## OpenSource - Corporate Analysis
<p float="left">
  <img src="/assets/img/corporate_analysis1.png" width="95%" />
  <img src="/assets/img/corporate_analysis2.png" width="95%" />
</p>
A opensource project. Visit it [here](https://github.com/RogerKimJazzLover/PYTHON-Corporate-Data-Analysis).

This opensource, API-based project:
1. gathers & organizes the financial statements of companies listed in KOSPI(Korean Composite Stock Price Index); over the period of past six years.
2. calculates essential & meaningful ***analytical data***. For example:
    - ROA, ROE, PER, 
    - Revenue/Operating Income/Net Income increase rate
    - Profit Status
3. visualizes those datas in various types of graphs. (Box plot, scatter plot, etc)

**⚙️ Frameworks and Packages Used**

**Financial Data Retrieval**
- `OpenDartReader` ***(API)***
- `FinanceDataReader`

**Data Analysis & Manipulation**
- `pandas`
- `numpy`

**Testing & Others**
- `pytest`
- `tqdm`
- `pickle`