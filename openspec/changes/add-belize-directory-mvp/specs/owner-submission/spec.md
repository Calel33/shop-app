## ADDED Requirements

### Requirement: Owner Create/Edit Listing
Owners MUST be able to create and edit a listing with required fields and validation.

#### Scenario: Save draft with validation
- **WHEN** an owner fills name, category, address, and places a map pin
- **THEN** they can Save Draft; missing required fields prevents saving with clear errors

### Requirement: Submit for Approval
Owners MUST submit listings for admin approval and see status updates.

#### Scenario: Submit succeeds
- **WHEN** an owner submits a valid draft
- **THEN** status becomes submitted and is visible in the dashboard

#### Scenario: Rejection with reason
- **WHEN** an admin rejects a submission
- **THEN** the owner sees status=rejected with a reason and can edit and resubmit

### Requirement: Status Tracking
The system SHALL show status chips for draft, submitted, approved, rejected.

#### Scenario: Status visible in owner dashboard
- **WHEN** an owner views My Listings
- **THEN** each listing shows its current workflow status
