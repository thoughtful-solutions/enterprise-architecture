# Enterprise Architecture Definitions

## Core Enterprise Components

### Value Stream
Represents an end-to-end sequence of activities that creates value for customers or stakeholders. Serves as a fundamental framework for understanding how value is delivered across the organization.

### Value Stage
A discrete step or phase within a value stream that transforms specific inputs into outputs. Each stage contributes to the overall value creation process with measurable metrics.

### Risk
A potential event or condition that could negatively impact organizational objectives. Includes assessment of both probability and impact along with mitigation strategies.

### Risk Control
A measure or action designed to modify risk through prevention, detection, or mitigation. Provides specific mechanisms to manage identified risks.

### Business Capability
A particular ability or capacity that a business requires to achieve its objectives. Represents what the business can do, independent of organizational structure or processes.

### Business Process
A collection of related, structured activities that produce a specific service or product. Describes how work gets done in the organization.

### Application
A software system providing specific business functionality to end users. Represents the technological implementation of business capabilities.

### Package
A deployable component or module of an application with specific functionality. Represents the smallest deployable unit of software in the architecture.

### Data Entity
A logical representation of information that is created, stored, and used by the business. Defines the structure and characteristics of business information.

### Technology
Infrastructure and platforms that support applications and data processing. Represents the technical foundation of the enterprise architecture.

### Organization
A structural unit within the enterprise with defined responsibilities. Represents the organizational context for capabilities and processes.

### Service
A defined offering that provides value to consumers through specific outcomes. Represents how capabilities are packaged and delivered to stakeholders.

### Role
A defined set of functions and duties assigned to individuals or teams. Represents who performs work and makes decisions in the organization.

### Responsibility
A specific duty or obligation assigned to a role. Defines what a role is accountable for and how it is measured.

## System Components

### IAM (Identity and Access Management)
Identity and Access Management system controlling authentication and authorization.

### RBAC (Role-Based Access Control)
Role-Based Access Control system implementing security policies.

### Directory Service
Central system managing user identities and organizational structure.

## Attribute Definitions

### Core Attributes
- **stakeholders**: Individuals, groups, or organizations that have a vested interest in the organization's activities, decisions, or outcomes. These can include customers, employees, shareholders, partners, regulators, and community members.
- **businessDrivers**: Forces, both internal and external, that influence an organization's strategies, objectives, and decisions. These can include market conditions, regulatory requirements, technological changes, customer demands, and competitive pressures that motivate the business to take action or make changes.
- **accountabilityLevel**: The degree and scope of responsibility for outcomes
- **artifacts**: Outputs or deliverables produced during development
- **buildConfigs**: Settings and parameters for compilation or assembly
- **businessOwner**: Individual or group responsible for business value and decisions
- **classification**: Security or privacy categorization tags
- **consumers**: Users or systems that utilize the entity
- **cost**: Financial or resource expenditure required
- **decisionRights**: Specific authorities granted for making choices or commitments
- **delegationRules**: Conditions and limits for transferring responsibilities
- **dependencies**: Other entities required for proper functioning
- **deploymentRules**: Specifications for how the entity should be deployed
- **description**: A detailed text explanation of the entity's purpose and scope
- **duration**: Time period required for completion or execution

### Performance and Quality Attributes
- **effectiveness**: Degree to which intended results are achieved
- **efficiency**: Measure of resource utilization versus output produced
- **escalationPath**: Sequence of roles to engage for issue resolution
- **impact**: Magnitude and nature of potential consequences
- **inputs**: Resources or data required for processing or transformation
- **integrations**: Collection of connected systems or interfaces
- **quality**: Measures of how well the entity meets various requirements

### Organizational Attributes
- **leader**: Individual responsible for direction and decisions
- **level**: Position in the organizational hierarchy
- **lifecycle**: Current phase in the entity's existence from creation to retirement
- **likelihood**: Probability of an event or condition occurring
- **location**: Physical or logical places where the entity exists
- **maturityLevel**: Degree of sophistication or development
- **metrics**: Specific measurements used to assess performance or success
- **mitigations**: Actions or controls to reduce risk or negative effects

### Technical Attributes
- **name**: A unique identifier string that serves as the primary label for the entity
- **outputs**: Results or products generated from processing or transformation
- **owner**: Individual or group responsible for management and decisions
- **parent**: Higher-level entity in a hierarchical structure
- **permissions**: Access rights and privileges assigned to roles
- **policies**: Rules governing behavior and access
- **providers**: Systems or groups that deliver the entity
- **requiredCertifications**: Formal qualifications needed for the role
- **requiredSkills**: Capabilities needed to perform the role effectively
- **retention**: Required period for maintaining the entity
- **roles**: Collection of defined functions and responsibilities
- **rules**: Specific constraints or conditions governing behavior

### Configuration and Management Attributes
- **schema**: Structure definition for data organization
- **scope**: Boundaries of authority and influence
- **securityProfile**: Security requirements and controls applied to the entity
- **sla**: Service Level Agreement defining performance expectations by metric
- **stages**: Discrete phases or steps in a sequence of activities
- **stakeholders**: Individuals or groups with interest in or influence over the entity
- **status**: Current state or condition in a lifecycle or process
- **strategicValue**: Importance to achieving organizational objectives
- **successors**: Roles that can assume these responsibilities
- **support**: Maintenance and assistance arrangements by type
- **syncRules**: Rules governing data synchronization
- **technicalOwner**: Individual or group responsible for technical implementation and operation
- **type**: Classification or category of the entity
- **value**: A quantitative or qualitative measure of the worth or importance
- **vendor**: External provider or supplier of the entity
- **verificationMethod**: Ways to confirm responsibility fulfillment
- **version**: Specific iteration or release identifier

## Attribute Types
- **single**: One value only
- **set**: Collection of unique values, unordered
- **ordered-list**: Sequence of values where order matters
- **map**: Key-value pairs