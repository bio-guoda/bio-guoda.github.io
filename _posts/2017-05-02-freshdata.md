---
layout: post
title:  "FreshData"
date:   2017-05-02
excerpt: "FreshData: Notifications of new data records"
project: true
tag:
- guoda 
- effechecka
- project
- eol
comments: false
---
**This project has been brought to a close and is no longer actively maintained. For more information about the history and context of this widget, please see the [github documentation](https://github.com/gimmefreshdata)**.

FreshData was developed by EOL to provide a way for researchers to know when new
data of interest becomes availible as well as for data providers to know what 
data researchers find interesting.

Users subscribe to FreshData monitors using [http://gimmefreshdata.github.io](http://gimmefreshdata.github.io).
Whenever new occurrence data is available for a monitor, subscribers are 
notified. At time of writing two notification mechanism are supported: email and
webhook.

Data providers can register data archives with FreshData using 
[http://archive.effechecka.org](http://archive.effechecka.org). Some data 
archives are imported once, while others are updated periodically. Whenever data
is added, FreshData monitors are updated and subscribers are notified.

Archives are stored in parquet files on GUODA infrastructure and monitors are
run as Spark jobs.

You can read more about [FreshData on its wiki](https://github.com/gimmefreshdata/freshdata/wiki).
