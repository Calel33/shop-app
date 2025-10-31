## ADDED Requirements

### Requirement: List-First Homepage Discovery
The system SHALL provide a list-first homepage with hero search and curated sections to enable quick discovery on mobile.

#### Scenario: Homepage populated
- **WHEN** a visitor opens the homepage
- **THEN** they see Hero Search (keyword, category, location), Featured Categories, Featured Businesses, and Latest Listings in that order

#### Scenario: Homepage empty states
- **WHEN** featured data is unavailable
- **THEN** the sections render graceful empty states without layout shifts

#### Scenario: Map preview link
- **WHEN** a visitor scrolls below the fold
- **THEN** they can access a Map preview or a clear link to the dedicated Map View

### Requirement: Search Results List View
The system SHALL render a list-first results page with filters and infinite scroll; nearest sort applies when location is set.

#### Scenario: Query with filters
- **WHEN** a visitor searches with keyword/category/location
- **THEN** results display with filters applied and support infinite scroll

#### Scenario: Nearest sort
- **WHEN** a location is provided
- **THEN** results preference favors nearest listings while preserving relevance

### Requirement: Listing Detail View
The system SHALL display complete business details with actionable contact and directions.

#### Scenario: Detail shows required fields
- **WHEN** a visitor opens a listing
- **THEN** they see name, category, short description, address, directions link, phone, website (if any), hours (if provided), images (≤5), and a static map preview or pin
