# USER ACCEPTANCE TEST PLAN  
**Microsoft Dynamics 365 Business Central**  
**TechGear Distribution Pte Ltd**

<br/>

## TEST EXECUTION SUMMARY

| Metric | Count |
|------|------|
| Total Test Cases | 127 |
| Passed | 121 |
| Failed | 3 |
| Blocked | 2 |
| Not Executed | 1 |
| Pass Rate | 95.3% |

<br/>

## Test Coverage by Module

- **Financial Management**: 35 test cases  
- **Sales & Service**: 28 test cases  
- **Purchasing**: 18 test cases  
- **Inventory & Warehouse**: 22 test cases  
- **Integrations**: 16 test cases  
- **Reporting**: 8 test cases  

<br/>

## Finance Test Case

| TC ID | Test Scenario | Module | Priority | Preconditions | Test Steps | Expected Result | Actual Result | Status | Tester | Date | Defect ID |
|---|---|---|---|---|---|---|---|---|---|---|---|
| TC-FIN-001 | Create sales invoice in USD with exchange rate | Finance | Critical | Customer exists; USD exchange rate configured | "1. Go to Sales Invoices<br>2. Create new invoice<br>3. Select customer (USD)<br>4. Add line item<br>5. Post invoice<br>6. Verify GL entries" | Invoice posted; GL entries created with correct SGD equivalent using daily exchange rate | As expected | Pass | David Tan | 2025-05-15 | |
| TC-FIN-002 | Automated bank reconciliation with MT940 file | Finance | High | Bank account setup; MT940 file available from DBS bank | "1. Import bank statement (MT940)<br>2. Run auto-match<br>3. Review matches<br>4. Post reconciliation<br>5. Verify bank account balance" | Transactions auto-matched (>90%); bank account reconciled; GL updated | As expected | Pass | Sarah Lim | 2025-05-16 | |
| TC-FIN-003 | Intercompany transaction between SG and MY entities | Finance | Critical | Both entities configured; IC partner setup complete | "1. Create IC sales order in SG entity<br>2. Post transaction<br>3. Switch to MY entity<br>4. Verify IC purchase order created<br>5. Post IC purchase<br>6. Run IC elimination report" | IC transaction flows between entities; elimination entries auto-generated for consolidation | Failed - IC partner not found | Fail | Michael Chen | 2025-05-17 | DEF-012 |
| TC-FIN-004 | Fixed asset depreciation calculation (straight-line) | Finance | High | Fixed asset registered; depreciation book configured | "1. Register new laptop (cost: $2,000)<br>2. Set useful life: 3 years<br>3. Set depreciation method: Straight-line<br>4. Run monthly depreciation batch job<br>5. Review FA ledger entries" | Monthly depreciation = $55.56 ($2,000 / 36 months); GL entries posted correctly | As expected | Pass | David Tan | 2025-05-18 | |
| TC-FIN-005 | Malaysia SST calculation on sales invoice | Finance | Critical | SST module enabled; Tax codes configured (6% SST) | "1. Create sales invoice for MY customer<br>2. Select taxable item<br>3. Verify SST auto-calculated<br>4. Post invoice<br>5. Run SST-02 report" | SST calculated at 6%; Tax amount = $600 on $10,000 sale; SST-02 report shows transaction | As expected | Pass | Jessica Wong | 2025-05-19 | |
| TC-FIN-006 | Multi-dimensional reporting (Dept + Cost Center) | Finance | Medium | Dimensions configured; Default dimension rules set | "1. Post invoice with Department = Sales, Cost Center = Retail SG<br>2. Run P&L by Dimension report<br>3. Verify amounts allocated correctly" | Transaction appears in Sales dept, Retail SG cost center; P&L balances match GL | As expected | Pass | Sarah Lim | 2025-05-20 | |
| TC-FIN-007 | Month-end close process (consolidated) | Finance | Critical | All transactions posted for the month; IC transactions complete | "1. Run month-end checklist<br>2. Review open transactions<br>3. Post accruals/deferrals<br>4. Run consolidation<br>5. Generate consolidated financial statements" | Month-end close completed in <2 days; Consolidated P&L and Balance Sheet accurate | As expected (1.8 days) | Pass | David Tan | 2025-05-22 | |

<br/>

## Sales Test Case

| TC ID | Test Scenario | Module | Priority | Preconditions | Test Steps | Expected Result | Actual Result | Status | Tester | Date | Defect ID |
|---|---|---|---|---|---|---|---|---|---|---|---|
| TC-SAL-001 | Create retail sales order from POS | Sales | Critical | LS Retail POS configured; Integration active | "1. Create sale in POS (item: Laptop, qty: 1, price: $1,500)<br>2. Complete payment<br>3. Verify order syncs to D365 BC<br>4. Check inventory reduction" | Sales order created in D365 BC; Inventory reduced by 1 unit; Revenue posted to GL | As expected | Pass | Store Manager | 2025-05-20 | |
| TC-SAL-002 | E-commerce order sync from Shopify | Sales | Critical | Shopify integration configured; Test order in Shopify | "1. Place order on Shopify website<br>2. Wait for sync (real-time)<br>3. Verify order in D365 BC<br>4. Check customer record created" | Order appears in D365 BC within 2 minutes; Customer auto-created; Inventory reserved | As expected (87 seconds) | Pass | Michael Chen | 2025-05-21 | |
| TC-SAL-003 | Three-tier pricing (VIP customer gets discount) | Sales | High | Customer assigned to VIP price group; VIP prices configured | "1. Create sales order for VIP customer<br>2. Add item (standard retail: $100)<br>3. Verify VIP price applied<br>4. Post order" | VIP price auto-applied ($80 = 20% discount); Order total correct | As expected | Pass | Sarah Lim | 2025-05-22 | |
| TC-SAL-004 | Credit limit check (order exceeds limit) | Sales | High | Customer credit limit = $10,000; Current balance = $8,000 | "1. Create sales order value = $5,000<br>2. Attempt to post<br>3. Review warning message" | System blocks posting with error: "Order exceeds customer credit limit"; Cannot proceed | Failed - no warning shown | Fail | David Tan | 2025-05-23 | DEF-015 |
| TC-SAL-005 | Sales return and refund processing | Sales | Medium | Original sales invoice posted; Return authorization enabled | "1. Create sales return order (ref original invoice)<br>2. Add return line (defective item)<br>3. Post return<br>4. Process refund<br>5. Verify inventory restocked" | Return posted; Credit memo issued; Inventory quantity increased; Refund payment created | As expected | Pass | Jessica Wong | 2025-05-24 | |

<br/>

## Integration Test Cases

| TC ID | Test Scenario | Module | Priority | Preconditions | Test Steps | Expected Result | Actual Result | Status | Tester | Date | Defect ID |
|---|---|---|---|---|---|---|---|---|---|---|---|
| TC-INT-001 | Shopify inventory sync (15-min batch) | Integration | Critical | D365 BC has inventory data; Shopify connected | "1. Update stock in D365 BC (reduce qty by 10)<br>2. Wait 15 minutes for batch job<br>3. Check Shopify inventory level<br>4. Verify sync log" | Shopify inventory updated within 15 minutes; Sync log shows success; No errors | As expected (12 min) | Pass | Michael Chen | 2025-05-25 | |
| TC-INT-002 | Payment gateway webhook (successful payment) | Integration | High | Payment gateway configured; Test card available | "1. Create e-commerce order<br>2. Process payment via gateway<br>3. Verify webhook received<br>4. Check payment posted in D365 BC" | Webhook received within 5 seconds; Payment auto-posted; Invoice marked as paid | Blocked - webhook endpoint unreachable | Blocked | Sarah Lim | 2025-05-26 | DEF-018 |
| TC-INT-003 | Power BI dashboard data refresh | Integration | Medium | Power BI workspace configured; Dashboards published | "1. Post new sales transactions in D365 BC<br>2. Trigger Power BI refresh<br>3. Verify dashboard updates<br>4. Check data freshness timestamp" | Dashboard data refreshed; Sales KPIs reflect new transactions; Timestamp updated | As expected | Pass | David Tan | 2025-05-27 | |

<br/>

## DEFECT TRACKING LOG

| Defect ID | Related TC | Severity | Description | Steps to Reproduce | Assigned To | Status | Resolution | Closed Date |
|---|---|---|---|---|---|---|---|---|
| DEF-012 | TC-FIN-003 | High | IC partner not found during transaction posting | Create IC sales order; select MY partner; attempt to post | Microsoft Partner | Fixed | IC partner master data was missing in MY entity. Added partner and retested successfully. | 2025-05-18 |
| DEF-015 | TC-SAL-004 | Medium | Credit limit check not triggering warning | Create sales order exceeding credit limit; try to post | Microsoft Partner | Fixed | Credit limit check was disabled in customer posting group. Re-enabled and tested. | 2025-05-24 |
| DEF-018 | TC-INT-002 | High | Payment webhook endpoint unreachable (404 error) | Process payment in gateway; webhook fails to reach D365 BC | Integration Dev | In Progress | Investigating firewall rules; endpoint URL may need to be whitelisted. | |

