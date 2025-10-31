## ADDED Requirements

### Requirement: Review Queue
Admins MUST have a review queue with filters and sorting to process submissions efficiently.

#### Scenario: Filter by category and date
- **WHEN** an admin opens the queue and applies filters (category, submission date)
- **THEN** the list updates accordingly showing only matching submissions

### Requirement: Approve/Reject Submissions
Admins MUST approve or reject submissions with optional edits and a rejection reason.

#### Scenario: Approve submission
- **WHEN** an admin approves a valid submission
- **THEN** the listing status becomes approved and is visible publicly

#### Scenario: Reject with reason
- **WHEN** an admin rejects a submission
- **THEN** they provide a reason and the listing status becomes rejected; the owner can edit and resubmit

### Requirement: Manage Categories/Tags
Admins SHALL manage taxonomy (add/edit/remove categories and tags).

#### Scenario: Update taxonomy
- **WHEN** an admin edits categories/tags
- **THEN** changes are persisted and available in owner forms and filters
