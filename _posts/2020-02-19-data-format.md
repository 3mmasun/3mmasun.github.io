---
layout: post
title: "Exploring Data Formats"
date: 2020-02-20 11:00:00 +0800
tags: [data-engineering]
# img: "/assets/img/machine.jpg"
description: explore pros and cons of different data formats
---

# JSON - key value pair
pros:
- readability
- serialize / deserialize tools
- some type
cons:
- not able to split up the file
- repeated keys for every record => wasted space
- not fully typed

# CSV
pros:
- readability
cons:
- not able to split up the file
- no types
- require pre-process to clean up unwanted strings

# avro
pros:
- binary
- typed
- schema attached
- fast to write
- schema evolution fully supported
cons:
- slow lookup
- slow aggregation

# parquet
pros:
- binary
- typed
- schema attached
- support predicate and projection push down
- fast lookup
- fast aggregation
- compressed well
cons:
- slow to write
- slow to update and delte

Credit to https://github.com/arunma/DataFormats-Scala