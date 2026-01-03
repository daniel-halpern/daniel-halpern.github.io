---
layout: page
title: Dry Cleaning Business Data Science
description: End-to-End Data Science Project to modernize my family's business' decision making from intuition to quantified data science.
img: assets/img/ZLdashboard_Business_Total_Redacted.png
importance: 1
category: work
related_publications: false
mermaid:
  enabled: true
  zoomable: true
---

My parents operate two dry cleaning locations. Like many small business owners, they spent over 10 years basing business decisions on gut feeling and intuition. While their veteran status in the industry served them well, they lacked concrete data. Furthermore, migrating to modern software wasn't an option; new POS systems are expensive, and the learning curve would have been too steep given their limited English proficiency. Their current workflow is a well-oiled, efficient machine so it's definitely not a good idea to fix what isn’t broken!

Instead, I decided to keep the legacy infrastructure and build a data and analytics layer on top of it using my software engineering and data science skills. Here is the project architecture:

{% include figure.liquid loading="eager" path="assets/img/ZLdashboard_Architecture.png" class="img-fluid rounded z-depth-1" %}

### 1. Reverse Engineering the POS Database Schemas

To begin, I created a Google Drive data lake to centralize and clean sales data from both stores. This was challenging because the stores ran on two different versions of the Royal Touch Bluu software:

- **Store 1:** Ran legacy V1.0 (c. 2010s). My mother stayed on this version as she found the interface familiar and easier to navigate.
- **Store 2:** Ran V2.0 (c. 2020s) with enhanced features.

With no documentation for the database schemas, my first step was to reverse-engineer the storage logic, unlock the password-protected databases, and identify the tables containing analytics-relevant information.

### 2. Exporting the Tables

I wrote custom scripts, Python for the Store 1’s `.mdb` database and PowerShell for the Store 2’s SQL Server, to extract specific tables. These run via Cron jobs to automate backups. I then wrote local cleaning and sanitization scripts to strip sensitive information and standardize features before exporting the data to the centralized cloud storage (Google Drive).

### 3. The Analytics Platform

The final step was building the analytics platform. I wrote scripts to visualize the data which led to immediate takeaways that are already impacting our business.

#### Quantifying the Impact of Winter Break

In over 10 years of business, my parents had never taken an extended vacation, fearing that a drop in revenue would threaten their financial stability. However, they had no data to back this up. Last winter (2024), they closed the shop for one week during the Christmas and New Year holidays, typically our slowest period.

With the revenue information normalized, we quantified that a one week closure costs approximately ~$1,000 in revenue. My parents found this to be a reasonable price to pay for a well deserved break after decades of constant work.

{% include figure.liquid loading="eager" path="assets/img/ZLdashboard_Business_Total_Redacted.png" class="img-fluid rounded z-depth-1" %}

#### Customer Analytics

We also identified our highest-spending customers and those with the highest spending potential (momentum or spending velocity). These customers have supported our family for years and now we can better understand their habits.

{% include figure.liquid loading="eager" path="assets/img/ZLdashboard_Christopher_Customer_Redacted.png" class="img-fluid rounded z-depth-1" %}

### Future Work

Now that the pipeline is stable, I am excited to uncover further insights. Currently, I am working on:

- **Churn Prediction:** Training a supervised model to flag high value customers who haven't visited in ~90 days and quantifying the potential revenue loss. The goal is to apply interventions, such as targeted discount outreach.
- **Market Basket Analysis:** Using unsupervised learning to discover items frequently bundled together to design pickup deals. One easy bundle that we can identify without ML are suits and ties; however, given my experience working at the cleaners, I suspect there may be other more interesting correlations like alterations and dry cleaning as some customers often bring in a newly purchased item for immediate alteration and cleaning.
- **A/B Testing Experimentation:** With granular data, I can now run controlled experiments. For example, as previously mentioned, a target discount outreach experiment may look like this:
  - _Hypothesis:_ Targeted discounts will reactivate at risk high value customers.
  - _Control Group:_ 50% of at risk customers receive no text.
  - _Treatment Group:_ 50% of at risk customers receive a text.
  - _Metric:_ Return rate within 7 days.

### Conclusion

With this data pipeline in place, the sky is the limit!
