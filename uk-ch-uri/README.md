# Design specification for UK-CH-URI

## Description

This is the design specification for the UK Companies House URI library API.

The official documentation of the API can be found (here)[https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/426891/uniformResourceIdentifiersCustomerGuide.pdf]

## Guidelines for writing an implementation

Implementations should offer be structured and follow the API design, but also follow the idiomic structure of the particular programming language. When these goals conflict, language idiomacy should prevail.

### Examples
The API documentation shows that the response contains a field CompanyName. This field is to be stored in the Company object, so naming object fields exactly as received from the API would result in API usage like; "Company.CompanyName". This is not idiomatic, a convention like "Company.Name" makes much more sense.

In the API design specification we'll use snake notation. However, field conventions should be done as appropriate for the particular langauge. In a language like Go, we should therefore use "RegAddress", while in Rust the appropriate convention would be "reg_address". 

## API Design

### Objects
objects are defined as **type** *field name:* corresponding value.
Optional means that the particular field/sub-object can be empty or not exist.

Check the official documentation for the exact purposes of the fields.

#### Company
- **string** name: CompanyName
- **string** number: CompanyNumber
- **object** reg_address: RegAddress
    - **string** care_of: Careof
    - **string** po_box: POBox
    - **string** address_line1: AddressLine1
    - **string** address_line2: AddressLine2
    - **string** post_town: PostTown
    - **string** county: County
    - **string** country: Country
    - **string** postcode: Postcode
- **string** category: CompanyCategory
- **string** status: CompanyStatus
- **string** country_of_origin: CountryofOrigin
- **date** incorporation_date: IncorporationDate
- **date** registration_date: RegistrationDate
- **date** dissolution_date: DissolutionDate
- **object** previous_name: PreviousName (optional)
    - **date** **date**: CONDate
    - **string** name: CompanyName
- **object** accounts: Accounts
    - **uint** ref_day: AccountRefDay
    - **uint** ref_month: AccountRefMonth
    - **date** next_due_date: NextDueDate
    - **date** last_made_up_date: LastMadeUpDat (optional)
    - **string** category: AccountsCategory (optional)
- **object** returns: Returns
    - **date** next_due_date: NextDueDate
    - **date** last_made_up_date: LastMadeUpDat (optional)
- **object** mortgages: Mortgages (optional)
    - **uint** charges: NumMortCharges
    - **uint** outstanding: NumMortOutstanding
    - **uint** part_statisfied: NumMortPartSatisfied
    - **uint** satisfied: NumMortSatisfied
- **object** sic_codes: SICCodes (optional)
    - **array** text: SicText
- **object** limited_partnership: LimitedPartnerships (optional)
    - **uint** gen_partners: NumGenPartners
    - **uint** lim_partners: NumLimPartners