# Enterprise Architecture Dashboards

## 1. Risk Exposure Dashboard

```mermaid
pie title Risk Distribution by Impact Level
    "High Impact" : 15
    "Medium Impact" : 45
    "Low Impact" : 40
```
```mermaid
pie title Risk Control Status
    "Implemented" : 65
    "In Progress" : 20
    "Not Started" : 15
```

### Data Sources and Interpretation

This dashboard visualizes [Risk](ea-glossary.md#risk) distribution across the enterprise. The data is sourced from:

- **Risk Impact Distribution**:
  - Derived from the `impact` attribute of [Risk](ea-glossary.md#risk) entities
  - Categorized by impact levels defined in `likelihood` and `impact` attributes
  - Links to affected [BusinessCapability](ea-glossary.md#business-capability) entities through the "threatens" relationship

- **Risk Control Status**:
  - Based on [RiskControl](ea-glossary.md#risk-control) entities
  - Tracks `effectiveness` and `status` attributes
  - Maps to `mitigations` attribute in [Risk](ea-glossary.md#risk) entities

## 2. System Lifecycle Timeline

```mermaid
gantt
    title Application Lifecycle Timeline
    dateFormat  YYYY-MM-DD
    section CRM System
    Current Version    :done, crm1, 2024-01-01, 2024-06-30
    Upgrade Planning   :active, crm2, 2024-05-01, 2024-07-30
    Implementation    :crm3, 2024-07-01, 2024-12-31
    section ERP
    Legacy System     :done, erp1, 2024-01-01, 2024-09-30
    Migration Prep    :active, erp2, 2024-07-01, 2024-10-31
    New System       :erp3, 2024-10-01, 2025-03-31
    section Data Warehouse
    Current Phase    :active, dw1, 2024-01-01, 2024-12-31
    Modernization    :dw2, 2024-10-01, 2025-06-30
```

### Data Sources and Interpretation

This timeline tracks the lifecycle of key [Application](ea-glossary.md#application) entities. Data is sourced from:

- **Application Status**:
  - `lifecycle` attribute of [Application](ea-glossary.md#application) entities
  - `version` tracking from [Package](ea-glossary.md#package) entities
  - `deploymentRules` from associated [Package](ea-glossary.md#package) entities

- **Technology Stack**:
  - [Technology](ea-glossary.md#technology) entities supporting each application
  - `vendor` and `version` attributes
  - `lifecycle` status of underlying technologies

## 3. Business Capability Maturity

```mermaid
pie title Capability Maturity Distribution
    "Level 5 (Optimized)" : 10
    "Level 4 (Managed)" : 25
    "Level 3 (Defined)" : 35
    "Level 2 (Repeatable)" : 20
    "Level 1 (Initial)" : 10
```
```mermaid
pie title Value Stream Performance
    "Exceeding Target" : 30
    "Meeting Target" : 45
    "Below Target" : 25
```

### Data Sources and Interpretation

This dashboard visualizes the maturity of [BusinessCapability](ea-glossary.md#business-capability) entities and their associated [ValueStream](ea-glossary.md#value-stream) performance:

- **Capability Maturity**:
  - Based on `maturityLevel` attribute of [BusinessCapability](ea-glossary.md#business-capability) entities
  - Influenced by `strategicValue` assessment
  - Connected to `businessDrivers` showing strategic alignment

- **Value Stream Performance**:
  - Derived from `metrics` in [ValueStream](ea-glossary.md#value-stream) entities
  - Performance of associated [ValueStage](ea-glossary.md#value-stage) entities
  - Tracks `efficiency` and `effectiveness` metrics

## 4. Technology Modernization Timeline

```mermaid
gantt
    title Technology Stack Modernization Timeline
    dateFormat  YYYY-MM-DD
    section Database Platform
    Oracle 19c Migration    :active, db1, 2024-01-01, 2024-09-30
    PostgreSQL Evaluation   :db2, 2024-07-01, 2024-12-31
    section Application Servers
    WebLogic Upgrade       :active, as1, 2024-03-01, 2024-08-31
    Container Migration    :as2, 2024-06-01, 2025-03-31
    section Integration Layer
    ESB Deprecation       :active, int1, 2024-01-01, 2024-12-31
    API Gateway Implementation :int2, 2024-04-01, 2025-02-28
```

### Data Sources and Interpretation

This timeline tracks the modernization of [Technology](ea-glossary.md#technology) components:

- **Platform Updates**:
  - Tracks `lifecycle` stages of [Technology](ea-glossary.md#technology) entities
  - Maps to `dependencies` in [Package](ea-glossary.md#package) entities
  - Considers `support` arrangements and vendor relationships

- **Integration Evolution**:
  - Based on [Service](ea-glossary.md#service) implementation changes
  - Tracks `sla` requirements and performance
  - Maps to [Application](ea-glossary.md#application) integration points

## Dashboard Update Frequency

- **Real-time Updates**:
  - Risk metrics from [Risk](ea-glossary.md#risk) and [RiskControl](ea-glossary.md#risk-control) entities
  - [Application](ea-glossary.md#application) status changes
  - [Service](ea-glossary.md#service) performance metrics

- **Weekly Updates**:
  - [Technology](ea-glossary.md#technology) lifecycle status
  - [Package](ea-glossary.md#package) deployment status
  - Integration health metrics

- **Monthly Updates**:
  - [BusinessCapability](ea-glossary.md#business-capability) maturity assessments
  - [ValueStream](ea-glossary.md#value-stream) performance metrics
  - Strategic alignment measures

## 5. EA Health Dashboard

```mermaid
pie title Application Lifecycle Distribution
    "Modern" : 35
    "Mainstream" : 40
    "Legacy" : 15
    "Sunset" : 10
```
```mermaid
pie title Technology Stack Status
    "Current" : 45
    "Supported" : 30
    "Deprecated" : 15
    "End of Life" : 10
```

### Data Sources and Interpretation

This dashboard provides a comprehensive view of enterprise architecture health metrics:

- **Application Portfolio Health**:
  - Derived from [Application](ea-glossary.md#application) entities' `lifecycle` attribute
  - Tracks `version` status across [Package](ea-glossary.md#package) entities
  - Maps to [Technology](ea-glossary.md#technology) dependencies

- **Business Architecture Status**:
  - [BusinessCapability](ea-glossary.md#business-capability) `maturityLevel` distribution
  - [ValueStream](ea-glossary.md#value-stream) efficiency metrics
  - Critical [Risk](ea-glossary.md#risk) exposure and mitigation status

```mermaid
gantt
    title Value Stream Cycle Time Analysis
    dateFormat YYYY-MM-DD
    section Order to Cash
    Current Cycle    :done, o2c1, 2024-01-01, 2024-01-15
    Target Cycle     :active, o2c2, 2024-01-01, 2024-01-10
    section Procure to Pay
    Current Cycle    :done, p2p1, 2024-01-01, 2024-01-20
    Target Cycle     :active, p2p2, 2024-01-01, 2024-01-12
```

## 6. Digital Transformation Progress Dashboard

```mermaid
pie title Digital Initiative Status
    "Completed" : 30
    "In Progress" : 45
    "Planned" : 25
```
```mermaid
pie title Technology Adoption Rate
    "High Adoption" : 40
    "Medium Adoption" : 35
    "Low Adoption" : 25
```

### Data Sources and Interpretation

This dashboard tracks digital transformation progress through:

- **Initiative Tracking**:
  - Maps to [BusinessCapability](ea-glossary.md#business-capability) enhancement projects
  - Tracks [Service](ea-glossary.md#service) modernization efforts
  - Measures adoption of new [Technology](ea-glossary.md#technology) platforms

```mermaid
gantt
    title Digital Initiative Timeline
    dateFormat YYYY-MM-DD
    section Cloud Migration
    Infrastructure    :done, cloud1, 2024-01-01, 2024-06-30
    Applications     :active, cloud2, 2024-04-01, 2024-12-31
    section Digital Workplace
    Collaboration Tools :done, dw1, 2024-01-01, 2024-03-31
    Remote Work Platform :active, dw2, 2024-02-01, 2024-07-31
```

- **Value Realization**:
  - Based on [ValueStream](ea-glossary.md#value-stream) `metrics`
  - Customer satisfaction tracking through [Service](ea-glossary.md#service) `sla` metrics
  - Employee feedback on digital tools adoption

## 7. IT Efficiency Dashboard

```mermaid
pie title IT Spend Distribution
    "Infrastructure" : 30
    "Applications" : 35
    "Services" : 25
    "Innovation" : 10
```
```mermaid
pie title IT Service Performance
    "Meeting SLA" : 75
    "Near Target" : 15
    "Below Target" : 10
```

### Data Sources and Interpretation

This dashboard monitors IT operational efficiency through:

- **Resource Utilization**:
  - [Technology](ea-glossary.md#technology) platform usage metrics
  - [Application](ea-glossary.md#application) performance indicators
  - Infrastructure capacity tracking

```mermaid
gantt
    title IT Project Delivery Timeline
    dateFormat YYYY-MM-DD
    section Infrastructure Projects
    Network Upgrade    :done, net1, 2024-01-01, 2024-03-31
    Security Enhancement :active, sec1, 2024-02-01, 2024-06-30
    section Application Projects
    CRM Upgrade        :active, crm1, 2024-01-01, 2024-07-31
    ERP Migration      :crit, erp1, 2024-04-01, 2024-12-31
```

- **Service Performance**:
  - [Service](ea-glossary.md#service) availability metrics from `sla` tracking
  - Incident resolution times from support systems
  - Project delivery metrics against planned timelines

## Data Quality and Governance

All dashboard data is subject to governance through:

- **Ownership**:
  - Clear mapping to `owner` and `businessOwner` attributes
  - [Role](ea-glossary.md#role)-based access through [RBAC](ea-glossary.md#rbac)
  - Defined `accountabilityLevel` for data maintenance

- **Quality Measures**:
  - Data `quality` attributes tracking
  - Regular verification through `verificationMethod`
  - Automated validation through [IAM](ea-glossary.md#iam) systems