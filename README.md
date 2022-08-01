# Release 0

## Table of Contents

* [Introduction](#introduction)
  * [About me](#about-me)
  * [About Credera](#about-credera)
* [Knowledge, Skills and Behaviours](#knowledge-skills-and-behaviours)
* [Table of Tickets](#table-of-tickets)
* [Ticket 1](#ticket-1)
  * [Project Background](#project-background)
  * [Ticket Background](#ticket-background)
  * [Learning and Research](#learning-and-research)
  * [Completing the Ticket](#completing-the-ticket)
  * [Problems and Solutions](#problems-and-solutions)
  * [Conclusion](#conclusion)

## Introduction

### About Me

My Name is Hotu, and I'm from New Zealand. Before landing a position as an apprentice with Credera I was a chef for about 7 years. When I was still in highschool and the dream of becoming a snowboard instructor, when I finished highschool I moved to a ski town in the hopes of becoming one.
Better planing would have told me that I had made the trip too late in the season. Desperate for a job I applied everywhere.My hopes and dreams were dashed, and not wanting to pack up and leave I applied to everywhere I could, luckily a couple guys owned a seasonal pop-up pizza joint in the center of town offered me a job - *after a bit of pestering from myself*. In the 3 and a half years I was a pizza chef I studied culinary arts and helped them build their business by managing sites and opening new sites, etc.
Needing a new challenge I decided to move to Japan and break away from pizza. There I met my Sous Chef who had worked in Michelin starred restaurants. He inspired me to push myself even further and after a year-ish in Japan I decided to go to London and really test my mettle.
I got a job at a 1 star restaurant which was the hardest work, but also the most gratifying. In 2020, as everyone is aware by now, the pandemic hit. The hospitality industry was devastated by the effects of the pandemic.
With a bunch of free time on my hands, I decided to learn how to do some basic coding through Free Code Camp, Codecademy, and Code wars. Restrictions were easing and I was called back into the kitchen where, I found that I no longer had the passion I once had for cooking. This prompted me to get serious about software development. I joined Makers Academy in July 2021, once finished I applied to a bunch of different jobs, one of which being this DevOps apprenticeship with Credera.

### About Credera

Credera is a consulting firm focused on strategy, innovation, data, and technology. As a part of Omnicom Precision Marketing Group, Credera's approximately 3000 consultants across the globe partner with clients ranging from FTSE 100 companies and public sector giants to emerging industry leaders from strategy to execution to create tangible business results. Credera's deep business acumen and technical expertise, combined with a deep dedication to building trusted relationships, unlock extraordinary business performance for their clients. Its mission is to make an extraordinary impact on its clients, people, and communities.

## Knowledge, Skills and Behaviours

| KSB Number | KSB Description | Which ticket(s) | Overview of how I met it | Ticket Date | Document Link |
|:----------:|-----------------|:---------------:|--------------------------|-------------|---------------|
| K7 | General purpose programming and infrastructure-as-code. | 1 | For this project I relied heavily on Terraform for the infrastructure-as-code(IAC) and used Python for the AWS Lambda. | 10/01/2022 | |
| K13 | Automation techniques, such as scripting and use of APIs. | 1 | I know how to use scripts to automate steps in a pipeline and when to implement automated testing and how to use software developer kits to make use of cloud provider API's | 10/01/2022 | |
| K17 | What an API is, how to find them and interpret the accompanying documentation. | 1 | An API is "application programme interface". It is a pre-existing block of code that allows to pieces of code to talk to each other, depending on your needs you can make your own API or make use of the million different API's out there. No point in reinventing the wheel. | 10/01/2022 | |
| S12 | Automate tasks where it introduces improvements to the efficiency of business processes and reduces waste, considering the effort and cost of automation. | 1 | I implemented a solution that would automatically tag AWS resources upon creation, saving time and money by pinpointing who created the resource and allowing you to calculate the cost for the resource that have been deployed. | 10/01/2022 | |
| S17 | Code in a general purpose programming language. | 1 | I used Python to implement the logic for the AWS Lambda. | 10/01/2022 | |
| S18 | Specify cloud infrastructure in an infrastructure-as-code domain-specific language. | 1 | I used Terraform to write up the IAC for AWS | 10/01/2022 | |
| B1 | Exhibits enthusiasm, openness and an aptitude for working as part of a collaborative community; e.g. sharing best practice, pairing with team members, learning from others and engaging in peer review practices. | 1 | The toughest part about this project was that I was mostly alone, about 95% solo work and 5% pairing. Nobody likes getting blocked, but when I did I really enjoyed having someone come in and share their knowledge with me. I really enjoyed raising PRs and having somebody tell me where I can make improvements and what I've done well, because, it gives me new goals work towards and how I can be a better DevOps engineer. | 10/01/2022 | |

## Table of Tickets

| Ticket number | Ticket |
|:-:|--------------------|
| 1 | ![Auto tagging ticket](./images/auto_tagging_ticket.png) |
| 2 | ![Terratest ticket](./images/terratest_ticket.png) |

## Ticket 1

### Project Background

When joining Credera, depending on client engagements at the time, generally you'll be assigned to the bench to help create/improve internal products, this is only while you're not on a client. While on the bench, I didn't have the opportunity to do much as part of a team.
Every Monday and Wednesday there is a bench stand up where we discuss progress made or blockers on tickets we've been assigned to. You based on your interests, if nothing takes your fancy you will get assigned a ticket based on your experience.

### Ticket Background

This is part of an epic and was created as a ticket. I chose the ticket as it looked interesting and I hadn't done anything like this before. I would assume there were meetings before I was assigned to the ticket, as it was created before I joined. Because I had no idea what I was doing, I broke the ticket down into 2 steps in the beginning, manually test to see if the requirements are even possible, and then automate the process.

### Learning and Research

I had done a weeks worth of Terraform in the training before going onto placement, so I had to learn more about Terraform. I had to deepen my knowledge on AWS.

### Completing the Ticket

Majority of this task was solo work, a couple of times I got stuck on something to do with Terraform or the way the AWS environment I was deploying to was configured.

In the beginning I had no clue if this was possible, so I spent a lot of time googling. I found a video of someone who had implemented something similar through the UI. Seeing this I created a diagram of how I thought it was working - *this is the end result, in the beginning it only referenced the creation of S3 buckets*

![Autotagger Diagram](./images/Autotagger-Diagram.png)

With this in mind, I converted the diagram into Terraform, adding the missing parts that are auto-generated/easily overlooked as it could be a simple click of a button through the UI. My first step was to create a Lambda that would trigger on a specific event, *eg. a user creates an S3 bucket*, and have the Lambda log something simple.

#### Trigger Evidence

![trigger evidence](./images/creation-event.png)

Once I had evidence that the creation events were triggering the Lambda, I could then implement the logic that would provide the created resources with new tags.
Using the AWS SDK for python, *Boto3*, I could easily hit the AWS API and create an S3 client, scrape the logs for the bucket name, then provide the S3 client the bucket name, and then with an S3 client built-in function provide the bucket the required tags.

#### Lambda Handler

![lambda handler](./images/lambda-handler.png)

#### Tagging function

![bucket tagging](./images/bucket-tagging.png)

Once this has been deployed, and you create an S3 bucket, when you check your newly created bucket you'll see that there are now tags attached to it:
![tagged bucket](./images/tagged-bucket.png)

Once I could tag a bucket, targeting other resources was very easy, it was just a matter of changing the Boto3 resource I needed.

I chose to use Python in this project for three reasons:

* I hadn't used it before, I wanted to challenge myself
* It had minimal setup versus Javascript when using the AWS SDK
* It's quick and easy to pick up
* It looks cleaner

I used Terraform as the IAC as that's what I had the most familiarity with thanks to Makers and their crash course on DevOps.

### Problems and Solutions

One of the problems I faced when trying to tag S3 buckets, was that Boto3 didn't have a way to cleanly add tags to the bucket, so it would overwrite any tags it already had. I got around this by retrieving the tags that were attached to the bucket on creation and adding them to the list of tags that I wanted to provide.

Another issue I faced when expanding this project to incorporate more than just S3 buckets was, not all AWS resource take tags in the same way, which made this frustrating when I wanted to follow best practices and not repeat code, eg. S3 buckets, the accepted tags are formatted like so:

```python
'TagSet': [
  {'Key': 'CreatedBy', 'Value': user},
  {'Key': 'CreatedOn', 'Value': current_date}
]
```

but if I tried to do the same with an EKS cluster, all it would accept is the following:

```python
{
  'CreatedBy': user,
  'CreatedOn': current_date
}
```

### Conclusion

I was able to implement auto tagging for 5 different resources, S3 buckets, EC2 instances, ECK clusters, ECS clusters, and Glue registries. I made it easy to implement the logic for other resources by documenting thoroughly the approach one should take.
I learned some basic use of Python, deepened my knowledge on Terraform and AWS
This has helped by allowing Credera to pinpoint when and who created a resource, and track how much these resources are costing the company.
