# Never Block, Never Copy: mirai + mori from Shiny to the Cluster

*posit::conf(2026) — Houston, September 2026 · Charlie Gao, Open Source, Posit PBC*

## Abstract

Most parallel R is batch-and-wait: send off your tasks, wait for the
slowest — and you're locked out while it runs. In a Shiny app, every user
freezes. There's a quieter cost: eight workers each need their own copy of
your data, so a 200 MB data frame becomes 1.6 GB to serialize, move, and hold
in RAM. Your laptop habits die at deployment.

This talk shows you how to fix both problems with two CRAN packages, mirai and mori, building a production-ready memory model for event-loop applications.
mirai keeps the event loop moving: it processes results as they arrive instead
of blocking, and it's first-class in Shiny. When many users show up at once,
mirai can put a hard cap on how much data waits in the queue. When that limit
is reached, it hands back control to your app rather than freezing every
session. mori, on the other hand, removes the pressure at source: put a
dataset into shared memory once and every worker maps the same pages, so
200 MB per worker collapses to a 200-byte reference, with no changes to your
downstream code.

The same app runs anywhere you have compute. A new HTTP launcher makes the
cloud, Kubernetes, and Posit Workbench as easy to reach as your own servers
over SSH or an HPC cluster through its scheduler, and moving between them
takes a single line of configuration.

Scale further. Scale safely. Never block, never copy — from your Shiny app to
your cluster.
