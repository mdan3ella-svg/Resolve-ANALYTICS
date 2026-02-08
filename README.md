Resolve | ANALYTICS — Documentation & Technical Specification

1. Project Overview

Resolve | ANALYTICS is a specialized AEC (Architecture, Engineering, and Construction) application tailored for Senior Auditors, Quantity Surveyors (QS), and Quality Analysts. It bridges the gap between site-level measurements, financial unit rate analysis, and quality compliance.

The application is built as a Single-File Portable Solution, ensuring that auditors can carry the full logic and interface in a single HTML file without external dependencies beyond standard CDN-hosted assets.

2. Core Modules & Logic

A. Dashboard (Real-Time Project Health)

Logic: Aggregates the lineItems data to calculate the Forecast Final Account.

Metrics:

Budget Utilization: Calculated by comparing current spent data against the total budget.

Trade Cost Distribution: A visual representation of cost centers based on BoQ categories (Structural, Architectural, MEP).

B. QS / Unit Rate Analysis (URA)

BoQ Management: Supports real-time editing of quantities. The updateQty function triggers a re-calculation of the total contract value across the entire state.

URA Drill-down: Implements a "Four-Factor" analysis model:

Material: Base cost + conversion factors (e.g., ready-mix volume).

Labor: Calculated via man-hours per unit × base craft rates.

Plant: Equipment duration × hourly/daily rates.

Markup: A standard 15% (adjustable) overhead and profit factor applied to the subtotal.

C. Structural Measurement Engine (Spec Calculator)

Formula: Volume (m³) = Length × Width × Depth.

SMM Logic: Follows Standard Method of Measurement (SMM) principles.

Wastage Factor: Includes a hard-coded 5% wastage allowance (gross = net * 1.05) to provide "Ordering Quantities" vs "Net Plan Quantities."

Cost Linking: Multiplies net volume by the current Grade 35 concrete rate ($185.50/m³) to provide an immediate budget impact assessment.

D. Audit & Compliance

NCR Registry: Tracks Non-Conformance Reports (NCRs).

Status Logic: Categorizes site outcomes into Passed, Warning, or Pending, allowing auditors to visualize quality risks that may lead to financial retentions or rework costs.

3. BIM Integration Methods (LOD 400)

Resolve | ANALYTICS is designed to ingest data from high-fidelity Building Information Models. The integration focuses on LOD 400 (Level of Development) where elements are modeled with specific assembly and quantity information.

Quantity Take-Off (QTO) Mapping: The app supports mapping BIM object IDs to BoQ line items.

IFC Compliance: Logic is structured to accept Schema attributes from Industry Foundation Classes (IFC).

BIM-to-Field Sync:

Geometry Extraction: Length, Width, and Height parameters from the model can be piped directly into the Spec Calculator.

Material IDs: Structural grades (e.g., C35/45) are matched against the Material Database to ensure the correct Unit Rate is applied.

Visual Audit: Future iterations allow for WebGL overlays to highlight cost-overrun zones directly on the 3D geometry based on the URA variance.

4. Automated Reporting & Export

The system includes a reporting engine designed for high-level audit submissions and cost-control meetings.

Variance Reports: Automatically generates a comparison between "As-Planned" costs and "As-Measured" costs.

Audit Trail: Every change made to a Unit Rate or Quantity is logged (locally in this version) to ensure a transparent financial history.

Export Formats:

PDF Summary: A professional snapshot of the Dashboard and Audit Registry for stakeholder review.

CSV/Excel: A full data dump of the BoQ and URA for further analysis in legacy financial software.

Compliance Certification: Automatically aggregates all "Passed" NCRs into a Progress Claim Verification report, justifying the release of monthly valuations.

5. Technical Stack

Framework: Vanilla JavaScript (ES6+).

Styling: Tailwind CSS (CDN) for responsive, utility-first design.

Typography: Inter Font Family (Google Fonts) for high legibility in financial tables.

Icons: Lucide Icons (CDN) for semantic interface cues.

State Management: Local variable-based state with DOM reconciliation via template literals.

6. Usage Instructions

Navigating the App

Use the left-hand sidebar to switch between modules. The active tab state is managed via the switchTab(tabId) function, which toggles CSS visibility classes.

Performing a Unit Rate Analysis

Navigate to QS / Unit Rate.

In the BoQ table, look for items with an Analysis icon (chevron).

Click the chevron to open the URA Detail View.

Review the breakdown of labor, material, and plant.

Use the Sensitivity Analysis sliders (simulated) to see how fuel or waste spikes impact the final audit rate.

Using the Calculator for Site Measurements

Navigate to Spec Calculator.

Input dimensions (Length, Width, Depth) in meters.

The Net Measurement updates instantly.

Refer to the Gross field for procurement (includes wastage).

Click Update BoQ to synchronize the measurement with the financial cost sheet.

7. Auditor's Best Practices

Variance Tracking: Regularly compare the "Forecast Account" on the dashboard against the original budget to detect early signs of cost creep.

Quality/Cost Linkage: Before approving a payment for a BoQ item, check the Audit & Compliance tab to ensure the corresponding NCR for that zone is marked as "Passed."

Sensitivity Checks: Use the URA view to stress-test rates against market volatility (e.g., steel price surges).

8. System Requirements

Browser: Any modern web browser (Chrome, Edge, Safari, Firefox).

Internet: Required for initial load of Tailwind and Lucide CDNs.

Deployment: Can be hosted on a local intranet, web server, or opened directly as a file from a mobile device or tablet.

Created by the Resolve | ANALYTICS Engineering Team
