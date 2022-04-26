---
title: "DevOps"
description: "DevOps"
#lead: "DevOps"
keywords: 
    - Dev Ops
    - CI/CD
contributors:
    - Adrian Woo 
date: 2022-03-02T00:00:00+00:00
lastmod: 2022-04-11T00:00:00+00:00
draft: false
toc: true
plotly: false
images: []
weight: 100
menu:
    docs:
        parent: "KnowledgeObjects"
---
## DevOps Overview
DevOps is a methodology that allows organizations to deliver software at a high velocity that is faster than traditional software development and deployment cycles. Under the DevOps model, development and operations teams are combined into one team where development and operation engineers share their priorities and processes with each other. Continuous integration, continuous delivery, and continuous deployment pipeline (CI/CD) is a software development approach that enables DevOps teams to develop and deploy software efficiently. 

## Why is DevOps important?
Historically, deploying software from development to quality assurance to the production environment has always been a difficult task for many organizations. There has been a disconnect between development and operation teams. Both teams working closely together clear a lot of confusion and overcome challenges much faster. In addition, the adaption of the CI/CD pipeline improves software development time drastically by deploying small code changes frequently. The acceleration of code release and deployment can improve overall code quality and efficiency which affects businesses’ profitability as a result.

## CI/CD Overview:

### Continuous Integration:
Continuous Integration is a development process that automatically builds and tests code as soon as developers commit code changes to a shared source code repository. This practice allows developers to detect errors and fix bugs early on. Developers check-in their code frequently throughout the day. CI improves code quality and development efficiency.

### Continuous Delivery:
Continuous delivery ensures all code changes are in a deployable state. It allows software release at any time without manually maintaining the environment. Continuous delivery automatically builds, tests, and stages code. Then, developers could manually approve and trigger the deployment process to the computing environment. 

### Continuous Deployment:
Continuous deployment automatically passes code changes through the pipeline and then deploys into a designated environment, such as production or QA. Continuous deployment is similar to continuous delivery which automatically builds, test, and stages code changes. Continuous deployment on the hand automatically deploys to the designated environment rather than requiring developers manually trigger the process.

### CI/CD Software Development Cycle:
Figure 1 shows the steps required for the CI/CD development cycle.

![image](https://dz2cdn1.dzone.com/storage/temp/12113457-devops-phases.png)

Figure 1: DevOps Cycle (Patel 2019)

## Benefit of DevOps:
- Increases the speed of the software development and deployment process

- Improves reliability with CI/CD (continuous integration/continuous delivery) practice to ensure each change is functional and safe

- Improves scalability when launching complex systems in different environments such as QA, testing, and production

- Improves security by using automated compliance policies, fine-grained controls, and configuration management techniques

- Improves quality of software applications which adds value to organizations



## Why is DevOps important to data science?
Data science and software development share a lot of similarities, even though the tools and skillsets required could be quite different. Both data scientists and software engineers go through the following cycle: plan, code, build, test, release, monitor, and feedback. They both struggle with the same problems when making changes to source code and deploying to production environments. Data scientists are experts in building models and data pipelines but they may not be an expert in the deployment process. DevOps engineers, on the other hand, may not have the same level of knowledge in data modeling as data scientists but they are experts in building environments and deploying software into the production environment. Having both teams work together can bridge the knowledge gap and smooth out the deployment process. Historically, DevOps was solely for application development. Now as the data field is maturing, data engineers and machine learning engineers are defining their own DevOp practice as DataOp and MLOps where they have more specific requirements and practices. The DevOps for Data Science article, it describes the difference between DevOps, DataOps, and MLOps.

An excellent video [DevOps for Data Science - Damian Brady](https://www.youtube.com/embed/bUTBBS1TECc) explains why data scientists need to implement DevOps practice in detail.

## Credit/Further Reading: 

What is DevOps? The ultimate guide – This is a complete guide to DevOps. The author explains different types of DevOps 
[https://searchitoperations.techtarget.com/definition/DevOps](url)

Secure and Scalable CI/CD Pipeline With AWS
[https://dzone.com/articles/secure-and-scalable-cicd-pipeline-with-aws](url)

Difference between CI/CD, Agile and DevOps
[https://www.browserstack.com/guide/ci-cd-vs-agile-vs-devops](url)

Stop messing up with CI/CD vs. DevOps and learn the difference finally
[https://www.itproportal.com/features/stop-messing-up-with-cicd-vs-devops-and-learn-the-difference-finally/](url)








