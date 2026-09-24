# Freight Dispatch Workflow

**Business Operations · Logistics · Process Design · AI-Assisted Development**

[Open the interactive demo](https://luisdelat710.github.io/acosta-fletes/)

## Problem

Delivery orders were dispatched by hand, without a consistent rule for which vehicle should carry a given load or a way to spot when two small routes could be combined into one larger trip. That produced avoidable trips, uneven vehicle usage, and no shared visibility into what was scheduled for the day.

## My role

I defined the vehicle-assignment rule, the consolidation logic, the role-based permissions for warehouse, logistics and management, and the status flow an order goes through from scheduling to delivery. I used **AI-assisted development** to implement the workflow. I do not present this project as evidence of independent software engineering. My contribution was translating the dispatch problem into explicit business rules, then reviewing the outputs against how the operation actually runs.

## Business rules

**Vehicle assignment**
- Internal shipment, weight ≤ 1,230 kg → **Nissan NP300**
- Internal shipment, weight > 1,230 kg → **Ford F-450**
- Marked as external freight → **Fletera externa**, regardless of weight

**Consolidation advisory**
When a new Nissan NP300 order is scheduled, the system checks existing Nissan NP300 orders for the same day and the same scope (Local / Foráneo). If another order is within 120 minutes and the combined weight exceeds 1,200 kg, it suggests consolidating both into a single Ford F-450 trip instead of running two.

**Roles and permissions**
- **Almacén** — advances an order's status
- **Logística** — creates and edits orders
- **Gerencia** — full access, including deleting orders and advancing status

**Status flow**
`Programado → En ruta → Entregado`

## Solution

The portfolio demo includes:
- Order scheduling form with live vehicle suggestion as weight and shipment type change
- Consolidation advisory prompt when two compatible Nissan NP300 orders overlap
- Role-based action visibility (view switcher included for demo purposes)
- Search and CSV export of scheduled routes
- Local browser storage for safe demo interaction

## Validation

The implementation was reviewed against the intended dispatch workflow: whether the weight threshold matched real vehicle capacity, whether the consolidation window and weight floor reflected when combining routes is actually worth it, and whether the permission split matched who is allowed to do what in the real operation.

## Data and confidentiality

This repository is a **sanitized portfolio recreation** of a real operating system used at Pisos y Azulejos Acosta. Client names, addresses, phone numbers and order history are simulated. No production credentials, customer data, or company database are included. The real system also includes an AI-assisted "Smart-Paste" feature that reads order details from a pasted screenshot of the internal ERP; that step depends on a private API and is described here for context rather than reproduced in the public demo.

## What I learned

A dispatch rule is only useful if it is explicit enough that anyone on the team would assign the same vehicle to the same order. Making the weight threshold and the consolidation window visible in the interface — instead of leaving them as tribal knowledge — was what actually reduced disagreements about which unit should take a route.

## Tools

HTML, CSS, JavaScript, browser localStorage, and AI-assisted development.

## What this demonstrates

- Logistics and dispatch process design
- Rule-based decision automation
- Role-based access design
- Consolidation / route-optimization logic
- Workflow status design
- AI-assisted implementation reviewed against operating needs

## Related case studies

- [Fleet Operations Review](https://github.com/luisdelat710/flotillaacosta) — daily unit reporting, fuel spend tracking and KPI compliance.
- [Pricing & Margin Decision Tool](https://github.com/luisdelat710/calculadoraprecio) — retail pricing rules, margin versus markup, and unit price validation.
- [Demand Capture & Operations Case Study](https://github.com/luisdelat710/demand-capture-operations-case-study) — frontline demand capture and normalization.
