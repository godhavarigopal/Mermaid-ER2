```mermaid
classDiagram
direction TB
    class SalesChannel {
	    +salesChannelID: UUID
	    +channelType: enum ChannelType
    }

    class Distributor {
	    +distributorID: UUID
	    +distributorNumber: String
	    +groupID: UUID
	    +class: String
	    +hasPortalAccess: Boolean
	    +hasPortalAccessDefault: Boolean
	    +activeFromDateTime: DateTime
    }

    class DistributorGroup {
	    +distributorGroupID: UUID
	    +name: String
    }

    class DistributorTeam {
	    +distributorTeamID: UUID
	    +name: String
	    +order: Int
	    +parentTeamID: UUID
    }

    class Agent {
	    +agentID: UUID
	    +agentNumber: String
	    +name: String
	    +status: enum AgentStatus
	    +role: enum TeamRole
	    +terminationType: enum TerminationType
	    +reactivationType: enum ReactivationType
    }

    class Product {
	    +productID: UUID
	    +name: String
	    +lifecycleStage: enum ProductLifecycle
    }

    class Party {
	    +distributorName: String
    }

    class BankAccount {
	    +bankAccNumber: String
	    +bankAccName: String
	    +bankAccCurrency: String
	    +bankAccAddress: String
	    +bankID: String
	    +branchID: String
	    +isPrimary: Boolean
    }

    class PaymentData {
	    +paymentTo: enum PaymentTo
	    +paymentCurrency: String
	    +paymentFrequency: enum Frequency
	    +heldPayment: Boolean
	    +minThreshold: Float
	    +canAgentsReadCommissions: Boolean
	    +umbrellaPaymentRule: Boolean
    }

    class ChannelType {
	    BRKR
	    InternalSalesforce
	    Aggregators
    }

    class AgentStatus {
	    ACTIVE
	    TERMINATED
	    SCHEDULED_TERMINATION
	    SOFT_DELETED
    }

    class TeamRole {
	    AGENT
	    MANAGER
	    ASSISTANT_MANAGER
    }

    class TerminationType {
	    IMMEDIATE
	    SCHEDULED
    }

    class ReactivationType {
	    IMMEDIATE
	    SCHEDULED
    }

    class ProductLifecycle {
	    DRAFT
	    PUBLISHED
	    ARCHIVED
    }

    class PaymentTo {
	    DISTRIBUTOR
	    AGENT
    }

    class Frequency {
	    MONTHLY
	    QUARTERLY
	    ANNUALLY
    }

	<<enum>> ChannelType
	<<enum>> AgentStatus
	<<enum>> TeamRole
	<<enum>> TerminationType
	<<enum>> ReactivationType
	<<enum>> ProductLifecycle
	<<enum>> PaymentTo
	<<enum>> Frequency

    SalesChannel --> "0..*" Distributor
    Distributor --> "1" Party
    Distributor --> "0..*" BankAccount
    Distributor --> "0..1" PaymentData
    Distributor --> "0..*" DistributorTeam
    Distributor --> "0..*" DistributorGroup
    DistributorGroup --> "0..*" Distributor
    DistributorTeam --> "0..*" Agent
    DistributorTeam --> "0..1" DistributorTeam : parentTeam
    Agent --> DistributorTeam : assignedTo
    Product --> "0..*" Distributor : released to


