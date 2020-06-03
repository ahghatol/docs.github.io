---
title:       TJQueue Introduction
description: Introduction to TJQueue, a Message queue for Joomla
path:        blob/master/docs/tj-queue
source:      tjqueue-introduction.md
hero:        TJQueue - Introduction
date:        2020-04-22
categories:
  - TJQueue
tags:
  - Joomla
  - queue
  - message
  - com_tjqueue
---

## Background
Several extensions have the need to do some heavy processing (inserting/updating lots of DB records, complex queries). A lot of this can be moved to background processing. TJ Queue allows creating these background jobs.

Any extension that wishes to use the background job queue can create a consumer that implements the 'job' they wish to perform. They can then 'produce' a message with the inputs needed by the job. The TJ Queue cron job will take care of fetching the messages and executing the job.

## Solution
This extension will provide facility to queue data and process queue as per priority.
Data will be deleted from the queue once it's executed successfully and the log will be stored in log file.
![Job Queue](https://user-images.githubusercontent.com/15344223/54255141-d565f180-457c-11e9-88f5-e0ea440ac786.png)
