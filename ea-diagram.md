# Enterprise Architecture Diagram

```mermaid
classDiagram
    direction LR
    
    %% Core Enterprise Classes
    %% ---------------------
    
    %% ValueStream Definition:
    %% Represents an end-to-end sequence of activities that creates value for customers or stakeholders.
    %% Serves as a fundamental framework for understanding how value is delivered across the organization.
    class ValueStream {
        name [single]
        description [single]
        value [single]
        metrics [set]
        stakeholders [set]
        stages [ordered-list]
        businessDrivers [set]  %% TOGAF: Business Motivation
    }

    %% ValueStage Definition:
    %% A discrete step or phase within a value stream that transforms specific inputs into outputs.
    %% Each stage contributes to the overall value creation process with measurable metrics.
    class ValueStage {
        name [single]
        description [single]
        inputs [set]
        outputs [set]
        duration [single]
        efficiency [single]
    }

    %% Risk Definition:
    %% A potential event or condition that could negatively impact organizational objectives.
    %% Includes assessment of both probability and impact along with mitigation strategies.
    class Risk {
        name [single]
        description [single]
        likelihood [single]
        impact [single]
        owner [single]
        mitigations [ordered-list]
    }

    %% RiskControl Definition:
    %% A measure or action designed to modify risk through prevention, detection, or mitigation.
    %% Provides specific mechanisms to manage identified risks.
    class RiskControl {
        name [single]
        description [single]
        type [single]
        effectiveness [single]
        cost [single]
        status [single]
    }

    %% BusinessCapability Definition:
    %% A particular ability or capacity that a business requires to achieve its objectives.
    %% Represents what the business can do, independent of organizational structure or processes.
    class BusinessCapability {
        name [single]
        description [single]
        maturityLevel [single]
        owner [single]
        strategicValue [single]
        status [single]
        businessDrivers [set] %% TOGAF: Business Motivation
    }

    %% BusinessProcess Definition:
    %% A collection of related, structured activities that produce a specific service or product.
    %% Describes how work gets done in the organization.
    class BusinessProcess {
        name [single]
        description [single]
        inputs [set]
        outputs [set]
        owner [single]
        metrics [set]
        lifecycle [single] %% TOGAF: Lifecycle Management
    }

    %% Application Definition:
    %% A software system providing specific business functionality to end users.
    %% Represents the technological implementation of business capabilities.
    class Application {
        name [single]
        description [single]
        vendor [single]
        version [single] 
        lifecycle [single] %% TOGAF: Lifecycle Management
        businessOwner [single]
    }

    %% Package Definition:
    %% A deployable component or module of an application with specific functionality.
    %% Represents the smallest deployable unit of software in the architecture.
    class Package {
        name [single]
        description [single]
        version [single]
        technicalOwner [single]
        dependencies [set]
        artifacts [ordered-list]
        buildConfigs [map]
        deploymentRules [set]
        securityProfile [map]
    }

    %% DataEntity Definition:
    %% A logical representation of information that is created, stored, and used by the business.
    %% Defines the structure and characteristics of business information.
    class DataEntity {
        name [single]
        description [single]
        classification [set]
        owner [single]
        retention [single]
        quality [map]
    }

    %% Technology Definition:
    %% Infrastructure and platforms that support applications and data processing.
    %% Represents the technical foundation of the enterprise architecture.
    class Technology {
        name [single]
        description [single]
        version [single]
        vendor [single]
        lifecycle [single] %% TOGAF: Lifecycle Management
        support [map]
    }

    %% Organization Definition:
    %% A structural unit within the enterprise with defined responsibilities.
    %% Represents the organizational context for capabilities and processes.
    class Organization {
        name [single]
        description [single]
        type [single]
        parent [single]
        leader [single]
        location [set] %% Zachman: Network (Where)
    }

    %% Service Definition:
    %% A defined offering that provides value to consumers through specific outcomes.
    %% Represents how capabilities are packaged and delivered to stakeholders.
    class Service {
        name [single]
        description [single]
        sla [map]
        owner [single]
        consumers [set]
        providers [set]
    }

    %% Role Definition:
    %% A defined set of functions and duties assigned to individuals or teams.
    %% Represents who performs work and makes decisions in the organization.
    class Role {
        name [single]
        description [single]
        type [single]
        level [single]
        requiredSkills [set]
        requiredCertifications [set]
        scope [single]
        successors [set]
    }

    %% Responsibility Definition:
    %% A specific duty or obligation assigned to a role.
    %% Defines what a role is accountable for and how it is measured.
    class Responsibility {
        name [single]
        description [single]
        accountabilityLevel [single]
        delegationRules [map]
        escalationPath [ordered-list]
        decisionRights [set]
        verificationMethod [set]
    }

    %% System Components
    %% ----------------

    %% IAM Definition:
    %% Identity and Access Management system controlling authentication and authorization.
    class IAM {
        name [single]
        type [single]
        policies [set]
        integrations [set]
    }

    %% RBAC Definition:
    %% Role-Based Access Control system implementing security policies.
    class RBAC {
        name [single]
        roles [set]
        permissions [map]
        rules [set]
    }

    %% DirectoryService Definition:
    %% Central system managing user identities and organizational structure.
    class DirectoryService {
        name [single]
        type [single]
        schema [map]
        syncRules [set]
    }

    %% Relationships
    %% ------------

    %% Value Stream Relationships
    %% Defines how value flows through the organization
    ValueStream --> ValueStage : contains
    ValueStage --> BusinessProcess : utilizes
    ValueStream --> BusinessCapability : requires

    %% Risk Relationships
    %% Shows how risks impact different architectural elements
    Risk --> BusinessCapability : threatens
    Risk --> Application : impacts
    Risk --> Technology : affects
    Risk --> DataEntity : endangers
    RiskControl --> Risk : mitigates
    Risk --> Responsibility : "assigned to"
    RiskControl --> Responsibility : "managed by"

    %% Business Architecture Relationships
    %% Defines core business structure and operations
    BusinessCapability --> BusinessProcess : realizes
    BusinessProcess --> Application : "supported by"
    Application "1" --> "1..*" Package : contains
    Package --> Technology : "runs on"
    Application --> DataEntity : processes %% Zachman What with CRUD arrows

    %% Organization and Role Relationships
    %% Shows organizational structure and responsibilities
    Organization --> BusinessCapability : owns
    Organization --> Role : defines
    Role --> Responsibility : has
    Role --> BusinessCapability : enables
    Role --> BusinessProcess : performs
    Role --> Application : uses
    Role --> Package : manages
    Role --> DataEntity : stewards

    %% Service Relationships
    %% Defines service implementation and delivery
    Service --> BusinessProcess : implements
    Service --> Application : "delivered by"

    %% System Implementation Relationships
    %% Shows technical system interactions
    IAM --> RBAC : enforces
    RBAC --> Role : implements
    DirectoryService --> IAM : feeds
  
    %% Attribute Types
    %% --------------
    %% single: One value only
    %% set: Collection of unique values, unordered
    %% ordered-list: Sequence of values where order matters
    %% map: Key-value pairs

    %% Attribute Definitions
    %% --------------------
    %% accountabilityLevel [single]: The degree and scope of responsibility for outcomes
    %% artifacts [ordered-list]: Outputs or deliverables produced during development
    %% buildConfigs [map]: Settings and parameters for compilation or assembly
    %% businessOwner [single]: Individual or group responsible for business value and decisions
    %% classification [set]: Security or privacy categorization tags
    %% consumers [set]: Users or systems that utilize the entity
    %% cost [single]: Financial or resource expenditure required
    %% decisionRights [set]: Specific authorities granted for making choices or commitments
    %% delegationRules [map]: Conditions and limits for transferring responsibilities
    %% dependencies [set]: Other entities required for proper functioning
    %% deploymentRules [set]: Specifications for how the entity should be deployed
    %% description [single]: A detailed text explanation of the entity's purpose and scope
    %% duration [single]: Time period required for completion or execution
    %% effectiveness [single]: Degree to which intended results are achieved
    %% efficiency [single]: Measure of resource utilization versus output produced
    %% escalationPath [ordered-list]: Sequence of roles to engage for issue resolution
    %% impact [single]: Magnitude and nature of potential consequences
    %% inputs [set]: Resources or data required for processing or transformation
    %% integrations [set]: Collection of connected systems or interfaces
    %% leader [single]: Individual responsible for direction and decisions
    %% level [single]: Position in the organizational hierarchy
    %% lifecycle [single]: Current phase in the entity's existence from creation to retirement
    %% likelihood [single]: Probability of an event or condition occurring
    %% location [set]: Physical or logical places where the entity exists
    %% maturityLevel [single]: Degree of sophistication or development
    %% metrics [set]: Specific measurements used to assess performance or success
    %% mitigations [ordered-list]: Actions or controls to reduce risk or negative effects
    %% name [single]: A unique identifier string that serves as the primary label for the entity
    %% outputs [set]: Results or products generated from processing or transformation
    %% owner [single]: Individual or group responsible for management and decisions
    %% parent [single]: Higher-level entity in a hierarchical structure
    %% permissions [map]: Access rights and privileges assigned to roles
    %% policies [set]: Rules governing behavior and access
    %% providers [set]: Systems or groups that deliver the entity
    %% quality [map]: Measures of how well the entity meets various requirements
    %% requiredCertifications [set]: Formal qualifications needed for the role
    %% requiredSkills [set]: Capabilities needed to perform the role effectively
    %% retention [single]: Required period for maintaining the entity
    %% roles [set]: Collection of defined functions and responsibilities
    %% rules [set]: Specific constraints or conditions governing behavior
    %% schema [map]: Structure definition for data organization
    %% scope [single]: Boundaries of authority and influence
    %% securityProfile [map]: Security requirements and controls applied to the entity
    %% sla [map]: Service Level Agreement defining performance expectations by metric
    %% stages [ordered-list]: Discrete phases or steps in a sequence of activities
    %% stakeholders [set]: Individuals or groups with interest in or influence over the entity
    %% status [single]: Current state or condition in a lifecycle or process
    %% strategicValue [single]: Importance to achieving organizational objectives
    %% successors [set]: Roles that can assume these responsibilities
    %% support [map]: Maintenance and assistance arrangements by type
    %% syncRules [set]: Rules governing data synchronization
    %% technicalOwner [single]: Individual or group responsible for technical implementation and operation
    %% type [single]: Classification or category of the entity
    %% value [single]: A quantitative or qualitative measure of the worth or importance
    %% vendor [single]: External provider or supplier of the entity
    %% verificationMethod [set]: Ways to confirm responsibility fulfillment
    %% version [single]: Specific iteration or release identifier
```

# Enterprise Architecture Glossary

The [Enterprise Architecture Glossary](ea-glossary.md) contains the definitions used
The [Mermaid.Live](https://mermaid.live/edit#pako:eNq9W21v3DYS_ivEAod7gR3krWmhDwe4TnsXXHMJkrQFWt8HWuLu8iKJKinZ2Rb57_fMkJQoiXLaGj2jaLxLckjO6zPD8S-70lRqV-zKWjr3XMuDlc1VK_BTaavKXptWfPPGf-P__6c_iUtjlfiq7ZXtrHZKXNJi5cbx89zPgsZ3sh7U294q2Yjnaq9bTXsV4_gb1VnlVNs7IVuh2uq8N-f4Rzj106DaUgmzFxIHvMFC5UR_lL0oQa7HhxsiLvbGinJwvWmUdQIfXC_fq6OpK3x-MO70VtkbrJH4T-yHtpINdpW12IMV6tbY90wIA1jVy7bS7UEczW3YRDtRqVrfKKsqnMcaR2fB6exBtvpnSbcKezGPZxf_xQ_QT4vNxI8OxGv1n-nrSrnS6o7lsB71R1h_36je6tJhRPXJ1-n9M2MHcOFHYyu6ynmtXTp8PWATBRWxdNWwmtn37tU_Lr4uxJdhgnhpIBO-tl_98apdCh07ZWV-AaXDdVWvcBzVkci6o4SC3er-qFvIx1_Yee6xyHsrWwcBNU64TpV6r0uh226A3ui2N8IMPX2YxP2VLI_-tqI0Lfh0PZDKYCqLDbeTdR02Yn0i1nfWlHQ5Ogi4K91g5XWtIqNzAqYN7ivfcJGFqMKVll9XONMGHbUHWzSs5rQYTIXzRrv3G2LpTA-b0DAKdYNfSDDgXcXzguWZoa5Eqw44wo2qT0I3HaxzZgZYbq7_S04F9jYJ5EVb1kPFFggn4hreYC-uDVgNvl_La13r_gQ3UEWqsjYwQi8MHOLg7w21gPUftJrLg-91X0nU-j2s_GhMlROTP9V6wNy2yubsczx03uKWYrkkRTX1hnS8PpLLYYeI8-Mu-tDCIUGrG1Pp_UlY4kJ_tGY4EFtZjph6hrm99_NnRGA62SSg19bcaBLQaGCNKo8Qq2vYbhrZkrJjCkjuNbalzdZCiLe4ryz6U6fySu51i93Qerw0LicjuIJ-cHfYRfRsl7KLqrhhJdL2uhxqCTmEiWQoWFbS72wncvSkwiKQIcYyC-GTNEQiNMw6ZyNJNLxlrwdXNRIqESArcwZvUakOITIY0ML0YB1D2Qc9Cf5sYSmZm95XVg2Ya0HoG9yu_g0WEm25_G4jxGXFth2pfmOgipNeB7-fF3hp6jpgJPDbqhpHrs4mTlcrgAK-VwOwi5xsyQF-6DJKBaP9JPbnzNtrrCbAwVjkoKADlWmhK-3dQGN5h_9rMNr0fHlkUmvY7qmsp1MlEvtmHHzJnoYixFpkF11X69JHgry4nNn3txIG4E6AFw2xG36N4NwojNGmAARLbzhsuoYQqBjcDDgmRkmCgBs9tqY2UFqYG2JCzSeVUT8Sew3mtYxU6RXuDQ1xYGOzA9alS8S9pZBa3auM3FMpvZbl-zvgn-pqc2JkVZqmg5Z7sIEYNtQe8QMFJlxiCDBKbya0TTm5BgBPIRYkuw04C5EfVSQYl7RwzBQfYc0zUcV73F9Mc2kkUY7UiVTp1YYpRWdfkndZ2BNFoj2cz12AXtcVIvJeHzCpkd2cMhhDAn4Dtq9TBVWyT4dj2WtSlml1KurnspdIErfjZTQVG-UzmopuCdHLCV4iy_K5HbtXpJ_4V3qLrMT1aRYPU_e5p2-81MfwR-sAXyzYowBUenJHqXkmm89EntznvlJngqSyEbD_Kt9JiVG7QfGnwXuqDVm8i74pL4sXLZLdOYc6BDOfVrEA3NB1xvap8TmeV4ErEU7gUHd7Rxb33lCSHUVNY2oqJWwaXHKDP87mNp3mPTxj5NyGZF4l4XsrbgXBgHfsp0I2vOAcu8KKNR4AXDl4T6cXYWYtlgVIpIxYfeh96SQJU14lsqBxdoE_CNoDWVMkyMhFySprK7VJbYsu_gMwNjKVQvxb9Yyk_vL9EY7xr2uRvA2IbCtGeRYbpBuWwEMEdj5H8oUDAAaw0g1ceYpZ1xingJkQ3jakQkhvznpYZOfDTeVNbqw3YZtMTcvLJd7iviJxtVzGhy0HNV154dECd-YDsyTX1J_iNxaSv4gxPnifwbPITfkusiBA7gr-kGt-vZLNViJlRKesd3KsEUSxATuppFdqx7t8CmXzyf8gta83kqaQOVZv3-u6XjE7jl4qAgGjs14G8dJk93RDSUZu7pBV6lu2Yvuo65AQp8Hmuo51mlRaUlgwcB2yb32yTIMU_GVZImr0jNXIN5GkyFA0Q4NQAKnmgpkf874iGk_A5LbSWZim8rcMyGluONhB1jz8WsJbb2GzqH1v9OG4Tq1g-qNYX6r-yCWprKTe-jznMkLp7Qp9sujFxcs8RuDyTqjDXbCSJPEu5lSlr_HU5BjlAMvBmuCJaR19ZWzOjmjbT8toKz6YWudgsEY0O9i1AczU-cuLy_wLBHTv_EtJCDNcNxawwl3HFI9TyACKx7PMlZE2-fT1SN3XzlPZRjvvjRb6ZJfwfIa_-QHH2NNd8ewSxydgEa7EpTy6DqW6oaI3xv-tgtIcJS93_d1CdeVRNavY405t-eaua79R3sLcUXd5hV8-SIjwGpNfGT3S9OSzr83tFNWX0cEvTF95zs__nj4KFGwkUrduNpWGaOaybFMIxLha_6xcnnKmaFeMtcVleT9_xbdHuhBdkAu3sZ5daYI4ZNwJKqc3AK_1YT3T3TwIuERpW7ucnJY6irDhck4C-Qshubq7nJLkZAWVaGR7AMqYJkWLpbm8qIgVbrUktYgXhbjaJYHqardBdL3Kl8MpLaVFq5KiuEhSnE_oXEkPrWNiOk_QEL6DZ_PLMuzPqxMEkqjTcnwtnKtdSGHGO9G6dM7V7tHVjlfitwcP_oYPsT6yVPb4_Uq-Vzs7wMHBfjIbrEQ9piIJshffE2bgNOjyzbfPobQWar2VahELGbvdZRKbJXRavcyx_NrZJptmAQS9NZ8PVQTYG5WUvsuq21Eup2T3Uy1Bp62pk25EPLyYOFeIwa0oTeL22r8cnwkPkeZW2splUq67zSGWyhe11SQnOvk1kVz-kuNyt569VP0p11qYc8BWL-ZHuUuZpgpIxA-UvPsXuzCXQBCLmeACSQ3CKEdm0peJhiyvsYq8NJcoFmKvVMWzJoTeh5dv8Q7RdwsYjl_74FyIV60KQdC09WkaVn0BdJS-hgyt_mkIk90ZPgasO65JsW8BGUxdHX4NUgDFj1WU4Dey70fHjsXABIX4lzqd-8N0UttUnabbTZjn7vaUcfAunF-Idwj2FSCl8i7AJ1H89jOzS0pRYpI_Ud6oyYKr4Q0Fq4K-sbXG1yJKc7nSUNFpTDfVl0B1XcclZvaESUPVRlIfC3HPV3WQDOg6lN8sv7k314ko84X8QrwY02padgD26aZbh6xsjFReKt4uQyI9bpCrfdKRA3zmZzB9I8uTKOkFcMwWBBBSQmVeaijEty42-bBxhbJlgE6xVoYNEgrJc3AhvtatbEvtr4eLmQGWJ9QHqrFr9vkxrx4p5NI03CRmviHXYfiMJKSl-ElcauR7EmZ5NDBS53spGqCSZpahZTNJMrLQduGFW-uGnoyJrG-EUZY1JR-bmOzy0QDqB-5YMUL9eE-mChVETBirLqCdklq_Ekz3D1kXESFkOUlAuCM3i1yrQGLG0nUOXnARCBiiJiRG1UlIpUaYWZSQQfrPsJnBdsYl5jnRXvbHwJw1EhLcT5tqfm2yklpFI1EfoJ0TtgetfK9BAXfDvqE38F66PLKLB7sZLAx174t54bG_Sqkt23MK8TJ2dewndfTq7G9BVezBhffX0VVMNO8qNcz9rc86-Y3zQEGcGICEc1C8cT2_-aLXBeeUBzjYofIsb2UfDj31DJGthu0mRUxfkwvCNXxD7wPpSWGpheF9QYyaHt9oEorLZH8Zk3CQFp-omBicBN2UojD8cnK2RVV55vyWPm9qk8y7u3oRQV4b59umMoVFkIdmWMq2Jj-1fnrAtQbLeZnvjpveArwJqA-QMQt3b00zNbFBwhY6bdUsgGQ6mwpq-Rn7rvyra6bxy5Tw2TZ1CfOqO8gcT44RD9bF1z6YbjlG98Qr8KnTCJ9rHBktjN9quyM_343BLBcfZw0HiXcONUN2uv4ZkaqR3IEWUbBsfVtGKIlOJDe7t-CqQnHaM4rSROf5zm0f3ISFodgnF_zIRHpWISHHF2DU2FtFTazTq4MbW1eJkYibjbQnUctrVfuYsA57s34NNjz2S1P3CYIVvBp131Ref36V8ZnfAReaqXqYt53Fs08h_olIq-y5t6mgN9wXGs3Gw-uYpk2EliW0Ipb0rI_d_nkLJ0bQXbwnsHecKM0qjeAfh74DtY1ScERQO8obHSrUcq43i1eQIuQQbuRQAC0BA-akN3vmHWMEv19zh5Cq69SmGkXdQjcSAW4YA_scZ9z1WgBURIKu_bbTYIt0Inhm2ow4tKKXvk3AYaUPWmF5Pz6_jFSmuJog0vWzN6ltiA4heHt10lxp8NaxYl1SW13GhfjENH9b2sRQNgd3OMrBOHTbu5mbzGnHlDglNc6C6pChvlCNaYsPMhQR10VGJpA-4xTiS35ct9rrRISgoXm23dcchZO8LdPJkYDxVGN830T0adwH4IWY4fX4ZliMybX34xfkvNni_Q3Bk9TZEtwu-6Bl16fgvCeyuR51hITYNM7hMHT6q85515D_e4GU5qInPnVeqW1yZYnRAjUP6daDh8BSbhzPsmLepzjFbhpQ84DK553i_QR8EmrZtsiC6hDG9szEsZ3Ue-yN_uuJ5OLBr-D6QvyDCsnPdci06G5ObRvFrM2BUCFDXz4Qu0J4VOfPJ62lMq1XKurdOSUgfVHeXztYNgWadbRmZQ0bPVO_LhxN9ZlMfWmstk57nWaGdzlPa7l_gtPX0zxFGdffLCR4QV6WpnhkAALe2fuPzZQNEK1bsPrICjjKfSI8b2IpxFcfoLMk_RiAPKhhC7Zbp9t4ZCzE9_LkQn_DXsN3L0sfQw1XUs8w2LLhJvGaug989Wk3kLdL0c7ubIckH5692hU7fkm62uG0jbra-ercXgK-UGHuI6bC3Zm3UI1dAUeqznb8QLMr9rBjfBo66I4Kf-MUp3Sy_cGY9OOu-GX3YVc8fvjg0bNHjx8-e_TZ06dP8OsXZ7vTrvjiyYNHD589efLZ5589ffbs84dPP57tfmYCjzBAP4-fPX787OHTJ5-f7RTs2tiX4S-s6J-P_wOT9ygT) contains a interactive editable version of this diagram