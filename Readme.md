# Fabric & Apparel Buying House ERP — Essential System & Interview Guide

---

## 📌 1. Project Overview & Architecture

### What is this project?
A commercial-grade, client-side **Fabric & Apparel Buying House ERP and Buyer Order Tracking Portal**. It provides end-to-end supply chain visibility from buyer purchase order placement, multi-factory split allocations, and 10-department manufacturing checkpoints to AQL 2.5 quality audits, partial container shipments, and live delivery countdown tracking.

### Technology Stack
- **Frontend**: Pure HTML5, CSS3, modern Vanilla JavaScript (ES6+).
- **Architecture**: Single-Page Application (SPA) with hash routing (`#dashboard`, `#orders`, etc.).
- **Persistence**: Browser `LocalStorage` with schema versioning (`v1.0.0`).
- **Dependencies**: **Zero** external libraries, zero frameworks (no React/Vue/Angular), and **zero backend** (no PHP/Node/MySQL required for demo).
- **Portability**: Runs immediately by double-clicking `index.html` or via any local server.

---

## 🧭 2. The 12 Core System Modules

| # | Module | Core Functionality |
|---|---|---|
| **1** | **Dashboard** | 8 dynamic KPIs, SVG Donut status chart, SVG production bar chart, 10-dept visualizer, factory capacity loads, upcoming shipments, and live audit timeline. |
| **2** | **Buyers** | Full CRUD, destination ports, Incoterms, payment terms, compliance standards, and **a live list of all purchase orders placed by that buyer**. |
| **3** | **Purchase Orders** | Multi-factory split allocations, color/size matrix breakdowns, real-time quantity summaries (Ordered, Allocated, Produced, QC Passed, Shipped, Remaining). |
| **4** | **Factories** | Monthly capacities (pcs/month), MOQs, lead times, active allocated order tracking, and capacity load utilization percentages. |
| **5** | **Departments** | Dedicated tracking across **exactly 10 departments** with department manager oversight, milestone dates, and progress percentages. |
| **6** | **Production Tracking** | Daily line output logs with dates and factory attribution; automatically updates department completion and order progress. |
| **7** | **Inventory** | Yarns, fabrics, trims, accessories, and packaging tracking with SKUs, dye lot numbers, warehouse bins, and **Low Stock Alert Badges**. |
| **8** | **Quality Control (QC)** | In-line and final AQL 2.5 audits, pass rate calculation, defect classification (stitching, shade variation, measurement tolerance). |
| **9** | **Shipments** | Multi-partial shipment support, ocean container numbers (`MSKU-8874120`), vessels, Bill of Lading (BL), and Airway Bill (AWB) tracking. |
| **10** | **Reports & Analytics** | 9 exportable reports with date filters and **one-click CSV downloads**. |
| **11** | **Activity Logs** | System-wide audit log tracking every user action with timestamps and user attribution. |
| **12** | **Settings & Admin** | Live company branding customizer, full JSON database backup export/import, default demo restore, and data wipe. |

---

## 🏭 3. The Exactly 10 Master Departments Pipeline

Each garment order progresses through 10 discrete gates:

```
[1. Merchandising & Order Planning]  -> Specs, costing, BOM, buyer delivery schedule
         ↓
[2. Sampling & Development]          -> Lab-dips, fit samples, buyer approvals
         ↓
[3. Procurement & Allocation]        -> Yarn booking, trims, factory split allocation
         ↓
[4. Fabric Production & Processing]  -> Knitting/weaving, dyeing, wash finishing
         ↓
[5. Fabric QC & Testing]             -> 4-point inspection, shrinkage, color fastness
         ↓
[6. Cutting]                         -> Fabric spreading, marker planning, bundle cutting
         ↓
[7. Sewing & Stitching]              -> Dedicated lines, daily output, rework tracking
         ↓
[8. Finishing & Ironing]             -> Thread trimming, steam pressing, measurements
         ↓
[9. Final QC, Packing & Warehouse]   -> AQL 2.5 audit, polybagging, carton packing
         ↓
[10. Export, Shipping & Docs]        -> Commercial invoice, customs clearance, Bill of Lading
```

$$\text{Progress \%} = \left(\frac{\text{Completed Quantity}}{\text{Target Quantity}}\right) \times 100$$
$$\text{Overall Order Progress \%} = \frac{\sum_{i=1}^{10} \text{Department}_i \text{ Progress}}{10}$$

---

## 🔒 4. Key Business Validation Rules

1. **Factory Allocation Guard**: Total allocated quantity across split factories must never exceed total order quantity.
2. **Production Progress Guard**: Completed quantity cannot exceed the applicable department target.
3. **QC Accountability**: Passed quantity + Failed quantity cannot exceed total inspected quantity.
4. **Shipment Eligibility Guard**: Shipped quantity cannot exceed eligible available or remaining order quantity. Goods must pass QC before booking.
5. **Relational Deletion Protection**: Buyers or factories with active orders cannot be silently deleted.

---

## 🌐 5. The Public Buyer Order Tracking Portal (`track.html`)

A dedicated client-facing tracking interface accessible at `track.html` or via direct link:
`track.html?order=PO-1001`

### Key Buyer-Facing Features:
1. **Live Delivery Countdown Clock**: Displays **Days : Hours : Minutes : Seconds** left until the delivery deadline.
2. **Current Stage Highlight**: Identifies which of the 10 departments is actively working on the order with a pulsating radar indicator.
3. **10-Stage Visual Stepper**: Displays completed checkpoints with green checkmarks and active checkpoints with real-time percentages.
4. **Quantity Reconciliation**: Displays Total Ordered, Produced, QC Passed, Shipped, and Remaining to Ship.
5. **Vessel & Container Logistics**: Displays Carrier, Vessel name, Container number, Bill of Lading, ETD, and destination port.

---

## 👔 6. Job Application & Interview Pitch Pack

### The 30-Second Elevator Pitch
> *"I designed and built a working **Fabric & Apparel Buying House ERP and Live Buyer Tracking Portal**.*
>
> *It replaces messy Excel sheets and WhatsApp guesswork by managing orders across **10 specialized departments**—from tech packs and multi-factory split allocations to daily sewing line output, AQL 2.5 QC audits, and container shipping.*
>
> *Most importantly, it gives international buyers a **live tracking link** with a real-time delivery countdown, current production stage, and container vessel details—guaranteeing complete supply chain transparency."*

---

### The 4 Pillars of Buyer Trust

1. **Zero Status Anxiety (Self-Service Live Tracking)**:
   - International buyers (H&M, Zara, Target) no longer need to send chasing emails. They check their order status independently in seconds.
2. **No Unauthorized Subcontracting (Factory Split Visibility)**:
   - Orders are visibly split across verified, compliant factories (e.g., 35k at Apex Mills + 15k at Horizon Fashion) with hard software validation.
3. **Guaranteed Quality (AQL 2.5 Compliance)**:
   - Defect classifications and pass rates ($95\%+$) are logged digitally. Goods cannot be shipped unless verified.
4. **No Last-Minute Delivery Surprises**:
   - 10 sequential department checkpoints catch delays 3 weeks ahead (during dyeing or cutting) instead of 3 days before the vessel departs, preventing costly **air-freight penalties** (\$30k–\$80k).

---

### Interview Questions & Model Answers

#### Q1: "How does your system prevent order delays?"
> *"Delays in apparel rarely happen in sewing—they originate in fabric dyeing, trims procurement, or marker planning. Because this ERP requires daily updates across all 10 departments, bottlenecks flag instantly. If Fabric Processing is 3 days behind, we can shift cutting bundles to a secondary allocated factory or schedule sewing line overtime weeks before the vessel cutoff."*

#### Q2: "Why did you build multi-factory split allocations?"
> *"Major retail buyers often order volumes that exceed a single factory's monthly capacity. In real buying houses, we split orders—for example, 35,000 pcs to a composite mill and 15,000 pcs to an activewear unit. The ERP manages this split under one master Buyer PO while tracking independent production lines and container dispatches."*

#### Q3: "What is your approach to buyer communication?"
> *"In apparel sourcing, buyer trust isn't built on polite emails—it's built on delivery predictability, quality proof, and zero surprises. By providing a live client-facing tracking portal, the buyer feels in control at all times."*

---

## 📚 7. Essential Apparel Industry Vocabulary

- **BOM (Bill of Materials)**: The complete recipe of raw materials, yarns, buttons, zippers, and packaging.
- **AQL 2.5 (Acceptance Quality Limit)**: The global apparel standard for final random inspections (Level II, Major 2.5, Minor 4.0).
- **4-Point Fabric Inspection**: Standard ASTM method for grading fabric roll defects per 100 square yards before cutting.
- **Marker Planning**: Computerized pattern layout to maximize fabric consumption and minimize cutting loss.
- **Incoterms**:
  - `FOB` (Free on Board): Seller delivers goods on board the vessel at port of origin (e.g., Chittagong).
  - `CIF` (Cost, Insurance & Freight): Seller pays ocean freight and marine insurance to destination port (e.g., Gothenburg).
  - `DDP` (Delivered Duty Paid): Seller delivers directly to buyer's warehouse with import duties paid.
- **Bill of Lading (BL) & Airway Bill (AWB)**: Official title of carriage documents issued by shipping lines or airlines.
- **L/C (Letter of Credit)**: Financial guarantee from buyer's bank payable upon presentation of compliant shipping documents.

---

## 🚀 8. How to Launch & Present the Project

1. **Direct Launch**:
   - Open `buying-house-erp/index.html` in any web browser.
2. **Public Buyer Tracking Portal**:
   - Open `buying-house-erp/track.html` or click the **"Buyer Portal"** button in the ERP header.
   - Test with pre-loaded demo POs: `PO-1001`, `PO-1002`, `PO-1003`, `PO-1004`, `PO-1005`.
3. **Local Server (Optional)**:
   ```powershell
   python -m http.server 8080
   ```
   Navigate to: `http://localhost:8080/buying-house-erp/index.html`
