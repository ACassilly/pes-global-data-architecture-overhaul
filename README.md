# pes-global-data-architecture-overhaul
Complete data layer orchestration overhaul for PES Global: SharePoint → Power Automate → Odoo/Shopify integration. Includes Gaurav's 32-category taxonomy, 254-manufacturer mapping, SharePoint List schemas, and automation scripts.

##  Overview

This repository contains the complete data architecture modernization plan for PES Global, consolidating fragmented systems into a unified data layer with SharePoint as the single source of truth.

**Created:** January 28, 2026  
**Status:** In Progress - Phase 1 (SharePoint Audit)

---

## 📋 Quick Links

### Documentation Resources
- **Claude AI Project (Cassilly Capital)**: [PES Global Data Layer Orchestration](https://claude.ai/chat/3de9938e-b845-4ddf-9428-5a375d039c0f)
- **Perplexity Analysis**: [SharePoint Structure Analysis](https://www.perplexity.ai/search/based-on-pes-global-s-sharepoi-5tV9XCv8SruScGlBVxhMIg)
- **Notion Brand Universe**: [254 Manufacturers Database](https://www.notion.so/2f30639f5451807a94d1dd7cf02678c1)
- **SharePoint**: Categories Re-Phrasing Final With SKU No. System.xlsx
- **Google Sheets (Legacy)**: [Taxonomy Reconciliation](https://docs.google.com/spreadsheets/d/18tRSl3DtET5prm1HdRAh_1-e5qYyuWJtxnodh8lepKU)

---

## 🏗️ Architecture Overview

### Current State Problems
1. **Fragmented Data Sources**: Taxonomy split across SharePoint, Google Sheets, Notion
2. **Manual Sync Required**: No automated data flow between systems
3. **Version Control Issues**: Multiple "master" copies
4. **No Audit Trail**: Can't track changes
5. **Google Sheets Dependency**: Unnecessary intermediate layer

### Proposed 3-Layer Architecture

```
┌─────────────────────────────────────────────┐
│  Layer 1: MASTER DATA (SharePoint)          │
│  - Product Categories (32 categories)        │
│  - Brand Registry (254 manufacturers)       │
│  - Product Master Data                      │
│  - SKU System (PES-[Home]-[Main])          │
└────────────────┬────────────────────────────┘
                 │
┌────────────────▼────────────────────────────┐
│  Layer 2: API ORCHESTRATION                 │
│  - Power Automate Flows                     │
│  - Azure Functions (Transform)              │
│  - Sync Queue Management                    │
└────────┬───────────────┬────────────────────┘
         │               │
┌────────▼──────┐   ┌────▼──────────┐
│  Odoo ERP     │   │  Shopify      │
│  - Inventory  │   │  - Storefront │
│  - Orders     │   │  - Collections│
└───────────────┘   └───────────────┘
```

---

## 📊 Gaurav's Taxonomy Structure

### Level 1 - Home Categories (9)
1. **Boilers** (BLR)
2. **Electric Vehicle Chargers** (EVC)
3. **Energy Storage Systems** (ESS)
4. **HVAC Systems** (HVAC)
5. **Parts & Accessories** (PA)
6. **Power Solutions** (PS)
7. **Solar Power Solutions** (SPS)
8. **Transformers** (TRF)
9. **Solar Energy Kits** (SEK)

### Level 2 - Main Categories (32 total)
- Boilers → Combination (CMB), Conventional (CNB), Condensing (CDB), Steam (STB), Hot Water (HWB), High-Efficiency (HEB)
- EVC → Level 3 (L3C), Level 2 (L2C), Level 1 (L1C)
- ESS → Battery Storage (BTS), All-in-One (AIO)
- And 23 more...

### SKU Format
`PES-[HomeAbbr]-[MainAbbr]`

Example: `PES-BLR-CMB` = Boilers - Combination Boilers

---

## 🗄️ SharePoint Structure (Current)

**Total Items**: ~2,000,000+

### Folders
```
/PES - Portlandia Electric Supply/
├── IT/
├── Marketing/
├── Operations/
├── Procurement/
├── Purchase Orders/
├── Sales/
├── SOPs/
├── Web Orders/
├── Legal/
├── Products/
│   └── Our Products - Latest-31-Aug-25/
│       └── Categories Re-Phrasing/
├── Pricing & Fulfillment/
├── Reports/
└── Odoo/ (3 subfolders)
```

---

## 📝 SharePoint Lists (Proposed)

### 1. PES_Taxonomy_Master
- TaxonomyID (TAX-XXXX)
- CategoryLevel1 (9 choices)
- CategoryLevel2
- ShopifyCollectionHandle
- OdooProductCategory
- ProductCount
- Manufacturers (Multi-select from Brand Universe)
- SyncStatus

### 2. PES_Product_Master
- ProductSKU (Unique)
- ManufacturerID (Lookup)
- TaxonomyID (Lookup)
- Pricing, Inventory, Specs
- OdooProductID, ShopifyProductID
- SyncStatus

### 3. PES_Brand_Universe
- BrandID (BRD-XXX)
- CarryStatus (CARRY-DIRECT, CARRY-DIST, EVAL, NOT-CARRY)
- Category, Website, Contacts
- OdooVendorID, ShopifyVendor
- PriorityTier (1-4)

### 4. PES_Purchase_Orders, PES_Sales_Orders, PES_Product_Pricing

---

## 🚀 Implementation Roadmap

### Phase 1: SharePoint Consolidation (Week 1-2) ✅ IN PROGRESS
- [x] Audit Gaurav's taxonomy (32 categories identified)
- [ ] Export SharePoint structure via PowerShell
- [ ] Create SharePoint Lists
- [ ] Build Power Query transformations
- [ ] Set up version control

### Phase 2: API Integration (Week 3-4)
- [ ] Odoo XML-RPC connection
- [ ] Category bulk import script
- [ ] Shopify API authentication
- [ ] Collection auto-generation

### Phase 3: Automation (Week 5-6)
- [ ] Power Automate flow deployment
- [ ] Error handling + retry logic
- [ ] Teams/Email notifications
- [ ] Monitoring dashboard

### Phase 4: Migration & Cleanup (Week 7-8)
- [ ] Archive Google Sheets
- [ ] Redirect team to SharePoint
- [ ] Staff training
- [ ] Process documentation

---

## 🔗 Related Projects

- **Master Catalog Thread**: Inverter Supply competitor analysis
- **ATLAS 42-Agent System**: Enterprise automation framework
- **Unified Implementation Roadmap**: CIEM, HRIS, Master Catalog

---

## 👥 Contributors

- **Alex Cassilly** - Architecture & Implementation
- **Gaurav Singh** - Taxonomy Design & Sourcing
- **Tanya Hahn** - Sales & Operations Data
- **Liam Cassilly** - IT Infrastructure

---

## 📅 Last Updated

**January 28, 2026, 12:00 PM EST**

*Note: This is a living document. All updates should be committed with detailed messages.*
