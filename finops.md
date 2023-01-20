# FinOps - from theory to practice

> FinOps is an evolving cloud financial management discipline and cultural practice that enables organisations to get maximum business value by helping engineering, finance, technology and business teams to collaborate on data-driven spending decisions. [^1]

This essay will provide a comprehensive introduction to FinOps, explaining why the framework exists and what are its founding principles. Then, it will summarise how the major public cloud providers – AWS, Azure and GCP – interpret the principles that back the FinOps framework. Lastly, two examples on how FinOps can be included in the daily job of DevOps engineers are described.

# From ITFM to FinOps 

FinOps falls into a broader discipline often referred as IT financial management (ITFM),
which can be defined as a discipline to govern the cost efficiency of IT.  

Traditionally, ITFM is executed centrally by finance or procurement departments to plan and control the overall spending of IT, mainly referred to as on-premises scenarios. Tech departments are marginally involved in the day-by-day operations because of the intrinsic nature of how IT purchases are done in traditional environments.

It is worth noting that different companies may have significant differences in the process. For instance, start-ups or small companies could have a lighter process to buy IT resources. Therefore, it is important to understand the core fundamentals behind the process, which will remain consistent across different sizes, industries, or stages of maturity.

 
At a high level, we can recognise 5 main steps that drive the procurement of IT resources in a traditional (i.e., on-premises) environment. 

1. The need for a new IT resource is raised typically by technology teams. 
2. The feasibility in terms of budget is checked by the finance office. Potentially, budget can be determined at the time of the request.
3. Tech and procurement work together to build up a list of potential providers. If only one provider is possible (i.e. Office 365 is provided only by Microsoft), this phase is skipped. 
4. The negotiation starts. This step varies largely. It may include tenders or can be as light as a phone call. Typically, procurement is in charge.
5. The contract is signed, and the resources are delivered. 
 
It is worth to notice that after the resources are paid for and delivered, there will be little or no interaction between tech and finance/procurement since there will be no need to agree and control costs after the delivery phase (step #5).
In fact, no operating costs are typically generated.

## The pay-as-you-go shift

Public clouds challenge this scenario and, therefore, require another methodology. 

If we go back to the NIST definition of cloud computing [^2], two (out of five) essential characteristics lead to the idea of finance.
For NIST, cloud is on-demand and metered, which both lead to the concept typically referred to as pay-as-you-go.
*Figure 1* pictures how the model works:

1. Users execute cloud operations on-demand.
2. Results being served as outputs to users or processes. 
3. Each cloud operation is metered, both for logging and invoicing purposes.
4. An invoice is sent to the users based on the real usage.

![Pay-as-you-go model](https://dtm-software-engineer.s3.eu-south-1.amazonaws.com/pay-as-yo-go.png)
Figure 1: *Pay-as-you-go model*

One of the most visible effects of the pay-as-you-go model is that financial operations become part of every DevOps engineer’s job because everyone’s actions become responsible and accountable for a share of the bill.
Being able to influence costs with their daily actions is a new capability for an engineer that causes however expectation problems.
The business expects engineers to be able to control cloud costs, while engineers keep their focus to guarantee the quality and the effectiveness of the delivery, which rarely includes thinking about costs.
 
FinOps creates a playing field for engineers and business teams in which the implications of the pay-as-you-go model are understood first and, then, controlled by everyone.

# The FinOps Framework 

Before diving into the framework, we need to highlight that the FinOps framework – as well as many other frameworks out there – can be seen as a reverse engineering of what many companies and teams were already doing in the past to control and plan cloud costs. Many of the concepts are not innovative per se. However, having a structured way to talk about financial operations eases the adoption of all the controls, processes, and best practices that have potential to bring concrete outcomes. 

The following sections present and comment on the most important peculiarities of the framework. For a full reference, please rely on the official sections of the FinOps Foundation 3. In the following sections, we will focus on the foundational principles that represent a guidance for every FinOps adoption.

## Principles

### Teams need to collaborate
FinOps, as highlighted in the previous section, is about making different teams speak the same language. To reach that point, strict collaboration among teams is pivotal, especially when it comes to finance and technology.

Looking at the procurement cycle of a public cloud is clear how – without communication – finance is left blind to the reasons why certain invoices must be paid. Establishing a strong relationship based on shared KPIs, reports, and automations will help to streamline critical processes such as forecasting, budgeting, and payment.

### Everyone takes ownership for their cloud usage

Public cloud is a distributed service by design, which leads to having a distributed consumption model – i.e., the pay-as-you-go model – in which a control plan is made available to the users through APIs. Everyone (with the appropriate permissions) is therefore able to control resources, hence, to generate costs.

Every team therefore must be responsible for the costs, because every team is responsible – by design – to generate them. Although a central team can provide financial insights, the ultimate goal of FinOps is about establishing a culture of cost efficiency and preventing waste in the first instance.

### A centralised team drives FinOps

Especially in the early phase of the FinOps adoption, a dedicated team (or dedicated time within the job of a person) can accelerate the adoption of best practices across the company. Also, a central team is typically used to deal with shared financial operations, such as capacity planning / reservation, budgeting and anomaly detection.

### Reports should be accessible and timely

Data consistency and integrity is probably one of the major issues in technology now considering the nature of most data (i.e., Big Data) that are generated at a higher speed than the one they can understand. Cloud costs fall in the same category with cloud providers providing data that are – more often than not – only eventually consistent.

For instance, AWS produces a snapshot of the consumption costs into an object called Cost and Usage Report (CUR). The CUR object is updated hourly, and it contains all the data points needed to calculate the costs of your usage from the beginning of the month. However, some cost dimensions, such as discounts and support costs, are factored only after the month ends. This means that the CUR becomes eventually consistent relative to the current month only 8-10 days after the current month ends.

Considering that finance typically deals with precision, this type of temporary inconsistency can create problems. It is important, therefore, when thinking of processes to design for consistency over time.

### Decisions are driven by business value of the cloud

Cloud adoptions are rarely driven by technological reasons. Maybe they start from technical people, but they grow and mature thanks to the business benefits that adopting the cloud brings to the business. In particular, the cloud represents an enabler for:

 - Business agility – by allowing deploying new features/applications faster and reducing errors, reducing time-to-market of revenue growth initiatives.
 - Operational resiliency – by benefiting of improving SLAs and reducing unplanned outage. Business continuity and disaster recovery become feasible options to achieve without upfront capital investment in your infrastructure.
 - Cost efficiency – by leveraging the economies of scale provided by cloud providers to reduce the cost of owning and running infrastructure.

### Take advantage of the variable cost model of the cloud.

Public cloud is founded on the pay-as-you-go principle, which does not just mean to pay resources when you need them. It means also to pay for the right number of resources when you need them. Being right means to optimise size and leverage all the options made available by cloud providers. Being able to move from a service billed by the time you use it to a service billed for how much you use it, for instance, gives you leverage that is very hard (or impossible) to have in traditional infrastructure contexts. (i.e., physical data centres). All options can and must be analysed in order to pick the right one.

# Implementing FinOps

The FinOps framework was built with the purpose to set principles and guidelines agnostic by specific cloud providers when it comes to implementation. However, it is not possible to decouple completely the theory and the practice since the feasibility of what the framework describes depends on the availability of specific features (i.e., capacity reservation) that the public cloud providers may or may not provide.

In particular, the framework identifies 6 domains to cover when it comes to executing FinOps and that – to some extent – cloud providers must make achievable:

 1. Understanding Cloud Usage and Cost
 2. Performance Tracking & Benchmarking
 3. Real-Time Decision Making
 4. Cloud Rate Optimization
 5. Cloud Usage Optimization
 6. Organizational Alignment

## Being well-architected

In order to provide users actionable advice, all hyper-scalers have developed frameworks to define a series of best practices to use in public cloud computing in the most efficient and effective manner. The way all of them approached the topic was by dividing the best practices into different domain or pillars.

Alongside with more technical pillars, such as security, operational excellence, reliability, and performance, financial operations is a domain that everyone covers. 4

Alongside best practices, cloud platforms provide services that can be used to implement the different FinOps domains. The following table shows what main services of all the three major cloud providers – AWS, Azure and GCP – allows each domain to be implemented.

FinOps Domain | AWS | Azure | GCP
------------- | --- | ------| ---
Understanding Cloud Usage and Cost | Cost Explorer | Microsoft Cost Management | Cost Management
Performance Tracking & Benchmarking | AWS Budget and Forecast | Forecasts in Azure Cost Management and Billing  | Cost forecast for Google Cloud Billing
Real-Time Decision Making | AWS Cost Anomaly Detection | Anomaly Detector | Cost Insight
Cloud Rate Optimization | Reservation, Saving Plans | Azure Reservation | GCP Committed Use Discounts 
Cloud Usage Optimization | Rightsize | Azure Advisor | Cloud instance rightsizing 
Organizational Alignment | AWS Organization | Subscriptions | Google Cloud resource

It is worth noticing that all providers cover with services for all the domains. Also, by embedding financial management into their (well) architecting frameworks, cloud providers highlight once more how pivotal cost is within system design when it comes to the public cloud. Cost becomes one of the pillars to consider and upon which to make informative decisions, with the same accuracy used to factor more traditional elements, such as security or operational excellence

# FinOps from the trenches

Let's now see how cost by design can take form in the everyday life of a DevOps engineer. At a high level, we can split the contexts in which costs are factored into two main categories: static and dynamic.

Static contexts are when costs are analysed theoretically. A typical example is the design phase of a new architecture in which DevOps engineer (and architects) can rely on static information – typically coming from cloud providers – to understand financial implications of their design choices.

Dynamic contexts, on the other hand, refer to moments in which our actions change the nature of the costs. One example is the update of the infrastructure code (IaC) that leads to altering the size or the nature of the cloud resources – hence the costs – used.

## FinOps when designing 

The design phase is arguably the most important phase of every project. In fact, an error at that level can generate a sequence of problems able to jeopardise the whole execution. On the other hand, DevOps often works to implement Agile principles, [^3] which often means requirements change over time. So, the question becomes how can we predict the cost of an architecture when the scope might not be entirely clear? The simple answer is that you cannot. That is why concepts like *architecture refinement* (as introduced by Michael Keeling) represents effective solutions. My design will change over time and so will my financial footprint. Engineers and architects must be ready to deal with changes (or different *views*, according to Keeling), understand the new scope, and pick the best solution.

The following is an example (based on a real case) on how to approach FinOps at the design level.

Let’s consider one of the simplest architectures: write objects to an object storage. Let’s call our design *Simple Architecture* and let’s use Amazon S3 as the storage service (the same reasoning can be applied to different cloud providers).

 - **Amazon S3**: the object storage service of Amazon Web Services. Through simple interfaces (i.e., GET, PUT), object storage-type of services like S3 allows users to store objects providing virtually no limits as to how much you can store.

The following image shows our *Simple Architecture*. The following assumptions/requirements are considered:

 - The application will run consistently for 4 hours per day. This gives us a daily volume of 10k/s * (4*60*60)s, or 144 million objects per day written to our destination.
 - Each object is 1Kb in size.
 - The writer process is not part of the analysis. It will be assumed to be able to run whatever business logic needed.  

![Simple Architecture](https://dtm-software-engineer.s3.eu-south-1.amazonaws.com/s3.png)

*Figure 2: Simple Architecture*

Now, in order to understand costs, we need first to understand how the services used charge for their usage. In particular, there are two main categories that you should consider:

 - **Time-based**: within the time-based category fall all those services that charge their main component of cost based on **how long** they are used.
 - **Volume-based**: within the volume-based category fall all those services that charge their main component of cost based on **how much** they are used.

Amazon S3 falls into the volume-based category. In fact, it charges based on 2 main KPIs:

 - **Amount of storage** = Different storage classes carriy different prices.
 - **No of Requests** = number of requests you make to the service. Example of requests are GET, PUT, COPY, LIST, POST, and Delete. GETs are 10x cheaper that PUT, COPY, LIST, and POST.

By using the numbers provided by AWS [^4], we obtain a total monthly cost of **$21,094.21**. 

The idea that you can describe your design from an economic perspective allows you not only to feel confident about the robustness of your idea, but it also gives you a baseline you can use to create a business case or discuss new business requirements, data driven. By analysing the KPI of costs, it is straightforward to see how the most impacting area of cost for Amazon S3 is the number of objects we store (PUTs) rather than the overall storage size. Therefore, one refinement view might be the one that writes objects in batches (by aggregating objects) in order to reduce the number of write operations (i.e., PUTs). Decreasing PUTs by a factor of 250 is fairly simple (from a writer perspective) and, by doing so, we reduce our monthly bill to **$178.21**. 

It is worth mentioning that semantically, the *Simple Architecture* has not changed. Of course, complexity of the system was increased, and other questions must be addressed, including the extent to which of the following points are worth the saving:

 - The increment in the overall complexity of our system.
 - The different approach and complexity needed to read a single object.
 - The effort needed to implement and maintain a more-complex solution.
 - The introduction of new services / business logic to manage the aggregation at writing level.

Answers to these questions **must** come from engineers and must be validated one by one. Reduction of cost must not be perceived as a must-have. Instead, being able to reduce costs must always be part of a perpetual effort to increase the efficiency of a system, the ultimate true goal for every engineering team.

## FinOps when committing

DevOps and Agile are about *"deliver working software frequently"*[^3], and deliver software frequently means dealing with code repository (aka commit changes) often. 

### Infrastructure as Code (IaC) 

Changes in infrastructure are reflected – often – in committing templates used to define the infrastructure. Referred to broadly as IaC, using declarative templates (i.e., using languages like Terraform) is a common approach to describe how the infrastructure looks when it comes to resources and/or connections. The template, then, is executed by an engine that is able to translate the code into instructions (i.e., API calls when it comes to the public cloud) that the cloud providers' control planes are able to manage.

From a FinOps perspective, this means that a template gives a static picture of how much our infrastructure costs. Changes at the IaC level possibly, then, reflect changes in the costs. Although templates are not able to cover volume-based costs, they represent an important point of entry and, eventually, gate keeping for cost governance.

### The toolchain

We will base our example on a very simple tool chain, which includes: 
 - Git
 - GitHub 
 - Infracost
 - Amazon Web Services (to show a possible integration) 

#### Git / Github

Git and Github represent out code repository, respectively those both local and remote. we are imaging a workflow in which a DevOps engineer who is responsible for changing IaC templates develops locally and then pushes the code to Github at 

The development uses the paradigm of branching and pull request. Let's see in more details one example of possible flow. 

 1. We commit our first version of a very simple template (using Terraform) that describe an Infrastructure (based on Amazon Web Services) that creates a simple virtual instance (EC2) of, say, 2 vCPU and 8GB of RAM (i.e. m5.large) . The initial version of the template is pushed to GitHub into the *main* branch1.	We commit our first version of a very simple template (using Terraform) that describe an Infrastructure (based on Amazon Web Services) that creates a simple virtual instance (EC2) of, say, 2 vCPU and 8GB of RAM (i.e., m5.large). The initial version of the template is pushed to GitHub into the main branch 1.	We commit our first version of a very simple template (using Terraform) that describe an Infrastructure (based on Amazon Web Services) that creates a simple virtual instance (EC2) of, say, 2 vCPU and 8GB of RAM (i.e., m5.large). The initial version of the template is pushed to GitHub into the *main* branch (@ https://github.com/michele-alessandrini/dtm-infracost/blob/main/create-ec2.tf)
 2. After a few tests, an increase in size of the instance is needed and a new version of the template is produced. Instead of overwriting the base, the developer creates a branch using git branch BiggerInstance and pushes the new branch to GitHub. The instruction creates a parallel branch named BiggerInstance.
 3. It then creates a pull request in GitHub that let other people of the team know that a new change has been pushed and needs a review before to be merged.
 4. Eventually, a merge is performed and BiggerInstance is merged back into *main*.

Now, in Now, in order to decide to move to #4, the team might perform some code review to see that the changes pushed will not cause any problems or that has been what proposed is coherent with the overall infrastructure strategy. What, however, is often missing is the analysis of the financial consequences of a new change. That is where Infracost enters the picture.

#### Infracost 

Infracost[^6] is a software component – both running as container in one environment or consumed as SaaS (Infracost cloud) and that allows users to analyse IaC templates (written in Terraform) and costify them. Most importantly, Infracost allows integrate with GitHub's pull request in order to generate cost analysis dynamically during a pull request, giving the team a information to use to decide whether a merge is possible.

While waiting for more native integrations, Infracost relies on GitHub Actions for integrations. GitHub actions let you orchestrate workflows by triggering execution of codes in response to an GitHub event. In this case, we link the even "on pull request" the link to Infracost SaaS. Security is implemented through an Infracost API Key stored in the GitHub secure registry.

The Github actions that allow Infracost to comment the pull request  with the information around costs does also replicate the core information on costs in a CSV file that is, eventually, merged to the main branch if the pull request is merged. t  

#### Amazon Web Services (AWS)

AWS is a public cloud provider that offer a variey of cloud services, ranging from traditional computing/storgae services to more managed and cloud native offering. 

In our example, we use AWS' native components to build a simple data pipeline to bring - everytime a commit happens in the main branch - the CSV file in the cloud so it can be used - application wise - to build dashboards.

To achieve that, we rely on:

 - AWS Code Pipeline to copy the repository to Amazon S3 each time a commit happens in the main branch.
 - Amazon Quicksight - a managed tool of business intelligence - to query the data copied and produce dashboards and reports.  

Figure 3 show the final dataflow. 

![AWS Data flow](https://dtm-software-engineer.s3.eu-south-1.amazonaws.com/infra-to-aws.jpg)

*Figure 3: AWS Data flow*

### The result

Infracost injects into the pull request all the information around new costs (in case of merge) and allows you to understand clearly the consequences of a merge from a financial perspective.

![enter image description here](https://dtm-software-engineer.s3.eu-south-1.amazonaws.com/infracost.png)

*Figure 3: Pull request summary in GitHub with costs information generated by Infracost*

You can see the live result also at https://github.com/michele-alessandrini/dtm-infracost/pull/2. 

Using the SaaS version of the service also allows access useful dashboards (as shown in the following pictures) to make sense of more complex context of CI/CD. 

![Summary of pull requests activities](https://dtm-software-engineer.s3.eu-south-1.amazonaws.com/infracost_1.png)

*Figure 4: Summary of pull requests activities*


 ![Summary of GitHub activities](https://dtm-software-engineer.s3.eu-south-1.amazonaws.com/infracost_2.png)

*Figure 5: Summary of GitHub activities and their financial impacts*

In terms of data, when a pull request is merged the CSV file containing the core information about costs is updated. You can find the data here: https://github.com/michele-alessandrini/dtm-infracost/blob/main/data/list.csv.

Figure 5 shows the CSV main fields. Fields' values are taken by the deatiled report that Infracost generated during the pull request and that it is available withing the Githb action in a json format.[^8] 

 ![CSV file updated](https://dtm-software-engineer.s3.eu-south-1.amazonaws.com/csv.png)

*Figure 5: CSV file is updated after every merge*
 
The file is then copied into the S3 bucket (see AWS reference architecture) and used as data source by Amazon Quicksight to generate meanginful dashaboards and reports. 

Figure 6 shows an example that shows how the differnt commit hashes affect the total monthly cost. The dahsboard can be useful to developers to understand immediately the impact of a change and act timely if there are problems. 

 ![Impact of commits on total monthly costs](https://dtm-software-engineer.s3.eu-south-1.amazonaws.com/dashboard.png)

*Figure 6: Impact of commits on total monthly costs*



# Conclusion

Transitioning to the public cloud exposes DevOps and cloud engineers to a new consumption model – the pay-as-you-go model – that breaks the common procurement cycle of IT. By doing so, such a move shifts to teams the accountability and responsibility of the costs of running cloud resources.

FinOps describes a framework that provides a set of practices and approaches needed to decode the ways in which the cloud works and makes the best out of all the benefits offered by the pay-as-you-go-model, such as elasticity and flexibility. DevOps engineers and the business are required to be able to communicate using the same language when it comes to cloud costs and FinOps creates the level playing field to achieve that.

All major cloud providers offer capabilities that allow embed FinOps into the everyday job of engineers. Two examples of how that translates into practice have been provided, although many others may suit different teams' needs and ways of working.

Engineers should focus on understanding that starting to analyse cost implications in their daily job can create a new perspective able to contribute to architectural decisions, to facilitate the communication with the business, and to exploit efficiently all the benefits of the public cloud.

**References:** 

[^1]: FinOps Foundation. 
[^2]: NIST on cloud computing  https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-145.pdf 
[^3]: https://www.agilealliance.org/agile101/12-principles-behind-the-agile-manifesto/
[^4]: Using https://calculator.aws/ 
[^5]: FinOps Framework https://www.finops.org/framework/principles/
[^6]: https://www.infracost.io/
[^7]: AWS Well Architected Framework - https://aws.amazon.com/architecture/well-architected/ Google Cloud Architecture Framework - https://cloud.google.com/architecture/framework Azure Well Architected Framework - https://docs.microsoft.com/it-it/azure/architecture/framework/
[^8]: Infracost JSON format - https://www.infracost.io/docs/features/json_output_format/