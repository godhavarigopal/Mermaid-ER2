```mermaid
erDiagram
    %% Claims Entity Relationships
    Claim ||--o| PolicyMember : "filed by"
    Claim ||--o| Policy : "belongs to"
    Claim ||--|{ BenefitClaim : "contains"
    Claim ||--o{ ClaimReversal : "may have"
    Claim ||--o{ Attachment : "may have"
    Claim ||--o| Organization : "provider"
    Claim ||--o| ClaimHandler : "handled by"
    Claim ||--o| ClaimApprover : "approved by"
    Claim ||--o| Customer : "claimant"
    Claim ||--o{ DiagnosisCode : "associated with"
    Claim ||--o{ OperationCode : "associated with"
    Claim ||--o{ GuaranteeOfPayment : "may have"
    Claim ||--o{ ClaimEventLog : "has history"
    
    BenefitClaim ||--o| Benefit : "references"
    BenefitClaim ||--|{ ClaimValue : "has"
    
    %% Entities
    Claim {
        String id PK
        String policyId FK
        String claimId
        String status
        DateTime createdAt
        String externalId
        String remark
        String issuerNumber
    }
    
    BenefitClaim {
        String id PK
        String claimId FK
        String benefitTypeId FK
        String benefitName
        String benefitDescription
        String currencyCode
        String remark
    }
    
    ClaimValue {
        Decimal billedAmount
        String billedCurrency
        Decimal approvedAmount
        String approvedCurrency
        String formattedBilledAmount
        String formattedApprovedAmount
        String unit
    }
    
    ClaimReversal {
        String claimId FK
        DateTime reversedAt
        String reversedBy
        String reason
    }
    
    Attachment {
        String id PK
        String entityId FK
        String fileName
        String mimeType
        String description
    }
    
    PolicyMember {
        String id PK
        String policyId FK
        String memberId
        String dependentOf
        String dependentOfPolicyMemberId
        Date startDate
        Date endDate
        String planId
        Boolean isRemoved
        Boolean isPrinted
        String certificateNumber
    }
    
    ClaimHandler {
        String id PK
        String name
    }
    
    ClaimApprover {
        String id PK
        String name
    }
    
    Organization {
        String id PK
        String name
        Boolean isActive
        String internalCode
    }
    
    Customer {
        String id PK
        String name
        String type
    }
    
    DiagnosisCode {
        String code PK
        String name
        String description
    }
    
    OperationCode {
        String code PK
        String name
        String description
    }
    
    GuaranteeOfPayment {
        String id PK
        String claimId FK
        String status
        DateTime issuedAt
        DateTime expiresAt
    }
    
    ClaimEventLog {
        String id PK
        String claimId FK
        DateTime timestamp
        String type
        String updateType
        String values
        String by
    } 
