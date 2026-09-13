# Building-permit-bottleneck-analytics
Analyzing building permit processing times to understand where delays occur, which permit types take longer, and where potential bottlenecks exist using Python, Pandas and SQL.

# Building Permit Bottleneck Analytics

### Understanding Building Permit Processing Delays Using Python, Pandas and SQL

## Overview

I wanted to work on a problem that is easy to understand from a real-world
point of view: **when someone submits a building permit application, how long
does it actually take to move through the process?**

For a property owner, contractor, or business, the waiting time can affect when
a construction or renovation project can move forward. At the same time,
different permit applications can naturally require different levels of review,
so a longer processing time does not automatically mean that something went
wrong.

This project looks beyond simple application counts and focuses on the
**processing time behind those records**. The aim is to understand how
processing time varies across permit types, locations, statuses, and time
periods, and to identify areas that may deserve further operational
investigation.

---

## Business Problem

A permit-processing system handles applications with different types,
characteristics, locations, and statuses. Because of this, processing time may
not be distributed evenly across all applications.

The main question I wanted to answer was:

> **Which types of building permit applications take longer to process, and
> where do the strongest potential bottlenecks appear?**

Rather than assuming the cause of a delay in advance, the analysis uses the
available data to identify patterns and areas that stand out.

---

## What I Wanted to Find

The project is built around a few practical questions:

- Which permit types receive the most applications?
- How long does it typically take for an application to be issued?
- Which permit types have the highest processing times?
- How different are average and median processing times?
- Has processing time changed over the years?
- Do processing times vary across neighborhoods?
- Which permit types combine high application volume with high processing
  time?
- Which areas appear to be the strongest candidates for further investigation?

---

## Dataset

The project uses the **San Francisco Building Permits** dataset.

The original dataset contains **198,900 records across 43 columns**, covering
permit information such as permit type, filing and issue dates, completion
dates, status, location, estimated cost, and other construction-related
attributes.

### Source

The dataset used for this project is available through Kaggle:

[San Francisco Building Permits Dataset](https://www.kaggle.com/datasets/aparnashastry/building-permit-applications-data)

The Kaggle dataset is based on publicly available San Francisco building-permit
data.

---

## Data Preparation

The raw dataset contained more information than was necessary for the main
analysis, so I narrowed it down to the fields directly related to permit
processing.

The preparation process included:

- selecting the most relevant permit, date, status, location, and cost fields
- converting the filing, issue, and completion fields into proper datetime
  values
- checking the logical order of permit dates
- handling inconsistent completion dates without removing the entire records
- removing exact duplicate rows
- handling missing neighborhood values
- retaining genuinely missing process dates rather than filling them with
  assumed values
- creating processing-time metrics for further analysis
- creating a filing year field
- renaming the final columns into SQL-friendly names

After removing **17,258 exact duplicate row occurrences**, the working dataset
contains **181,642 records and 11 analysis-ready fields**.

---

## Key Metrics

Two main metrics are used throughout the project.

### Days to Issue

The number of days between the date an application was filed and the date it
was issued.

```text
Days to Issue = Issued Date - Filed Date
