# Diff-in-Diff-Omni-Channel-Retail-Growth-Strategy

## Business Context

Home & Kitchen (H&K) launched a Buy Online, Pick Up in Store (BOPS) initiative to better integrate its online and brick-and-mortar channels. Under BOPS, customers can place an order online and pick it up at a nearby store, potentially changing shopping convenience and fulfillment behavior across markets. Because BOPS is tied to the online channel, leadership is interested in whether BOPS improves online performance—especially in markets where store proximity makes pickup feasible.

## Business Problem

Initial comparisons of average weekly sales before vs. after the BOPS launch suggest declines in both online and brick-and-mortar sales. However, simple pre/post comparisons are not sufficient to attribute changes to BOPS because they do not account for market-wide trends or time effects (e.g., seasonality). The key question is whether online sales changed differently in markets with store proximity (where BOPS is available in practice) relative to markets without nearby stores, after BOPS was introduced.

Analysis window (per case):
- Pre period: April 11, 2011 – October 10, 2011
- Post period: October 11, 2011 – April 2012

## Project Goal

Estimate the incremental impact of BOPS availability on online sales using a Difference-in-Differences (DiD) design at the DMA-week level. The analysis will compare online sales trends in DMAs within 50 miles of a store (close=1) versus DMAs farther away (close=0) before and after BOPS (after). Results will be delivered as (1) a defensible causal estimate of the BOPS effect on online sales under DiD assumptions, (2) supporting trend and pre-trend diagnostics, and (3) a dashboard for stakeholders.

This project will also produce descriptive summaries of brick-and-mortar sales (store-week) to provide channel context, while clearly separating descriptive results from the causal inference scope.

## Business Value

This project delivers value in two ways:

**1. Decision support:** Provides evidence to inform whether H&K should keep, expand, or modify BOPS by quantifying how online sales changed in BOPS-exposed markets relative to non-exposed markets during the same time period.

**2. Process improvement through reproducible analytics:** Implements a repeatable Databricks workflow that ingests the raw data, applies consistent cleaning and QA gates, materializes analysis-ready tables (did_panel, did_results, and dashboard aggregates), and enables a visualized dashboard reporting layer for ongoing consumption.

## Dataset Spec

**1. Online Sales Data**

Grain (unit of analysis): 1 row per DMA × week

Primary key: (dma_id, date) or (dma_id, year, week)

Time coverage: April 2011 – April 2012 (per case window)

Columns: 

- dma_id — Designated Market Area identifier
- date — week-ending date
- year, month, week — calendar fields
- after — 1 if week is after BOPS launch; 0 otherwise
- close — 1 if DMA is within 50 miles of a store; 0 otherwise
- sales — total online sales for the DMA-week (USD)

**2. Brick & Mortar Data**
Grain (unit of analysis): 1 row per store × week

Primary key: (id_store, date) or (id_store, year, week)

Time coverage: April 2011 – April 2012 (per case window)

Columns: 

- id_store — store identifier
- date — week-ending date
- year, month, week — calendar fields
- usa — 1 if store is in the U.S.; 0 if Canada
- after — 1 if week is after BOPS launch; 0 otherwise
- sales — total brick-and-mortar sales for the store-week (USD)