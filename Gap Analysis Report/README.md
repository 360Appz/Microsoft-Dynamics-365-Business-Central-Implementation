# GAP ANALYSIS REPORT  
**Microsoft Dynamics 365 Business Central Implementation**  
**TechGear Distribution Pte Ltd**

<br/>

## SUMMARY STATISTICS

| Metric | Count | % |
|------|------:|---:|
| Total Requirements | 127 | 100% |
| Standard D365 BC Functionality | 89 | 70% |
| Configuration Required | 28 | 22% |
| Custom Development Required | 10 | 8% |

### Development Effort Summary

| Category | Count | Effort |
|--------|------:|-------:|
| Zero Effort (Standard) | 89 | 0 hours |
| Low Effort (Configuration) | 18 | 144 hours |
| Medium Effort (Custom) | 7 | 280 hours |
| High Effort (Complex Custom) | 3 | 240 hours |
| **Total Estimated Effort** |  | **664 hours** |

<br/>

## Detailed Gap Analysis

| Req ID | Business Requirement | Priority | D365 BC Standard | Gap Type | Solution Approach | Effort (hrs) | Cost Estimate | Dependencies | Risk Level |
|------|----------------------|----------|------------------|----------|------------------|-------------:|--------------:|--------------|-----------|
| FIN-001 | Multi-currency support (SGD, MYR, USD) | Critical | Yes | None | Standard functionality | 0 | $0 | None | Low |
| FIN-002 | Intercompany transactions with eliminations | Critical | Yes | Configuration | Configure IC setup, chart of accounts mapping | 16 | $1,600 | Chart of Accounts finalized | Medium |
| FIN-003 | Automated bank reconciliation (MT940) | High | Yes | Configuration | Configure bank statement import, matching rules | 8 | $800 | Bank provides MT940 format | Low |
| FIN-004 | Fixed assets with depreciation | High | Yes | None | Standard functionality | 0 | $0 | None | Low |
| FIN-005 | Budget vs Actual reporting | Medium | Yes | None | Standard functionality | 0 | $0 | None | Low |
| FIN-006 | Malaysia SST calculation and filing | Critical | Add-on | Configuration | Install SST localization, configure tax codes | 24 | $2,400 | SST module licensing | High |
| FIN-007 | Singapore GST and Peppol e-invoicing | Critical | Add-on | Configuration | Configure GST, enable Peppol connector | 16 | $1,600 | IRAS registration complete | High |
| FIN-008 | Multi-dimensional reporting (Dept, Cost Center) | High | Yes | Configuration | Configure dimensions and default dimension rules | 8 | $800 | Dimension structure defined | Low |
| SAL-001 | Unified order entry (Retail, E-comm, B2B) | Critical | Partial | Custom | Develop custom order entry screen with channel field | 40 | $4,000 | Channel definitions | Medium |
| SAL-002 | Three-tier pricing (Retail, Wholesale, VIP) | Critical | Yes | Configuration | Configure customer price groups and sales prices | 8 | $800 | Pricing matrix approved | Low |
| SAL-003 | Automated credit limit checks | High | Yes | None | Standard functionality | 0 | $0 | None | Low |
| SAL-004 | Sales commission calculation | Medium | No | Custom | Develop commission calc engine, monthly report | 60 | $6,000 | Commission rules defined | Medium |
| INV-001 | Multi-location inventory tracking | Critical | Yes | None | Standard functionality | 0 | $0 | None | Low |
| INV-002 | Transfer orders between locations | Critical | Yes | Configuration | Configure transfer routes, in-transit accounts | 8 | $800 | Location codes defined | Low |
| INV-003 | Automated reorder point suggestions | High | Yes | None | Standard functionality | 0 | $0 | None | Low |
| INV-004 | Bin management in warehouse | Medium | No | Out of Scope | Deferred to Phase 2 | 0 | $0 | N/A | N/A |
| INT-001 | Shopify order sync (real-time) | Critical | No | Custom | Develop REST API connector for order import | 80 | $8,000 | Shopify API keys | High |
| INT-002 | Shopify inventory sync (15-min batch) | Critical | No | Custom | Develop scheduled job for inventory export | 40 | $4,000 | Shopify API keys | Medium |
| INT-003 | LS Retail POS integration | Critical | Yes | Configuration | Configure LS Retail connector for D365 BC | 24 | $2,400 | LS Retail licensing | High |
| INT-004 | Payment gateway webhook | High | No | Custom | Develop webhook receiver for payment confirmations | 32 | $3,200 | Gateway API docs | Medium |
| INT-005 | Power BI data model | High | Partial | Custom | Build Power BI data model and DAX measures | 60 | $6,000 | KPI definitions | Low |

<br/>

## DEVELOPMENT EFFORT BREAKDOWN BY MODULE

| Module | Standard | Configuration | Custom | Total Hours | Total Cost |
|------|---------:|--------------:|-------:|------------:|-----------:|
| Financial Management | 40 | 64 | 0 | 64 | $6,400 |
| Sales & Service | 15 | 8 | 100 | 108 | $10,800 |
| Purchasing | 8 | 8 | 0 | 8 | $800 |
| Inventory & Warehouse | 18 | 16 | 0 | 16 | $1,600 |
| Integrations | 0 | 24 | 212 | 236 | $23,600 |
| Reporting & BI | 8 | 8 | 60 | 68 | $6,800 |
| Compliance & Localization | 0 | 40 | 0 | 40 | $4,000 |
| **TOTAL** | 89 requirements | 28 requirements | 10 requirements | **664 hours** | **$66,400** |

<br/>

## GAP-RELATED RISKS & MITIGATION

| Risk ID | Gap/Requirement | Risk Description | Likelihood | Impact | Risk Score | Mitigation Strategy | Owner |
|------|------------------|------------------|-----------|--------|------------|---------------------|-------|
| R-001 | Shopify Integration | API rate limits may throttle real-time order sync | Medium | High | High | Implement retry logic with exponential backoff; monitor API quotas | Integration Lead |
| R-002 | Malaysia SST Module | SST rules may change before go-live | Medium | High | High | Partner with local tax consultant; build flexible configuration | Finance Lead |
| R-003 | Multi-channel Orders | Custom order entry may not handle all edge cases | Low | High | Medium | Comprehensive UAT with real-world scenarios; phased rollout | BA Lead |
| R-004 | LS Retail Connector | POS downtime during cutover | High | Critical | Critical | 2-hour cutover window at 2am Sunday; full rollback plan ready | Project Manager |
| R-005 | Data Migration | 5 years of QuickBooks data may have inconsistencies | High | High | High | Data cleansing workshops; staged migration with validation checkpoints | Data Lead |
