
```mermaid
erDiagram

    Customer {
        string customerId
        string externalReference
        string status
        string name
        string openingDate
        string referenceCurrency
        string language
        string customerSegment
        string[] personList
        string purposeOfRelationship
        object externalAssetManager
    }

    Person {
        string personId
        string externalReference
        enum personType
        string language
        string openingDate
        string givenName
        string middleName
        string lastName
        string title
        string gender
        array nationalities
        string civilStatus
        string dateOfBirth
        string dateOfDeath
        string dateOfMarriage
        string countryOfBirth
        object tinList "tinNumber, tinCountry"
        object legalPerson "organisationName, legalForm, lei, domiciliaryCompany" 
    }

    CustomerPersonRelation {
        string id
        enum relationType
        string cardinality
        string personId
        string relatedCustomerId
        string purposeOfRelationship
        boolean soleBeneficialOwner
    }

    person2personRelation {
        string id
        enum type
        string personId
        string relatedPersonId
        string relation
        string relationOverride
        boolean personAssociation
        string personAssociationName
        string personAssociationType
    }

    Address {
        string addressId
        string personId
        string externalReference
        enum type
        string addressName
        boolean isDomicile
        string language
        boolean isMailingAddress
        object salutationDetails
        string department
        string streetName
        string buildingNumber
        string buildingName
        string floor
        string postBox
        string room
        string postcode
        string townName
        string townLocationName
        string districtName
        string countrySubDivision
        string country
        string address 
    }

    Contact {
        string id
        enum medium
        enum prio
        string content
    }

    Document {
        string id
        string customerId
        enum group
        enum type
        enum status
        date issueDate
        string content
    }

    Education {
        string highestDiploma
        integer graduationYear
        string institute
        string studyProgramme
        object educationInformation
    }

    Employment {
        string companyName
        object companyDomicile
        object[] companyCountriesOfBusinessList
        string companyDetail
        integer companyNumberOfEmployees
        number companyAnnualTurnover
        string industry
        object roleOrPosition
        profession profession
        string domicile
        number shareholdingInPercent
        object period
        integer yearOfRetirement
        integer sharedholderSinceYear
        string mandate
        string additionalInformation
        object employmentInformation
    }

    Wealth {
        string sourceOfWealth_type
        object sourceOfWealth_amount
        object[] sourceOfWealth_countriesOfOrigin
        object sourceOfWealth_additionalProperties

        object totalWealth_amountTotalNetAssets
        object totalWealth_referenceYear
        object[] totalWealth_assetAllocation

        object totalIncome_amountYearlyIncome
        object totalIncome_referenceYear
        object[] totalIncome_sourceOfIncomeList
    }

    FundFlows {
        object amountExpectedInflows
        object amountPlannedTotalAssets
        object amountExpectedTurnover
        integer numberOfInflows
        integer numberOfOutflows
        object[] recurringCounterpartyList
        object[] initialAmountList
        object[] expectedFundFlowList
    }

    CorporateInsider {
        string corporateInsiderAssociation
        string relation
        object position
        string companyName
        string isin
    }

    MajorShareholder {
        string majorShareholderAssociation
        string relation
        string companyName
        string isin
    }

    Risk {
        enum politicalStatus
        boolean fatcaStatus
        boolean fatcaDomicile
        boolean fatcaBirthplace
        boolean fatcaGreenCard
        boolean fatcaSubstantialPresenceTest
        boolean fatcaOtherReasons
        object countryOfDomicile
        object[] taxDomicileList "taxDomicile"
    }

    %% Beziehungen

    Customer ||--|{ CustomerPersonRelation : hasMultiple
    Customer ||--o{ Document : hasMultiple
    CustomerPersonRelation }o--|| Person : hasMultiple
    person2personRelation }o--|| Person : hasMultiple
    person2personRelation }o--|| Person : isRelatedPerson

    Person ||--o{ Address : hasMultiple
    Person ||--o{ Contact : hasMultiple
    Person ||--o| Employment : hasOne
    Person ||--o| Education : hasOne
    Person ||--o| Wealth : hasOne
    Person ||--o| Risk : hasOne
    Person ||--o{ FundFlows : hasMultiple
    
    Risk ||--o{ CorporateInsider : hasMultiple
    Risk ||--o{ MajorShareholder : hasMultiple
