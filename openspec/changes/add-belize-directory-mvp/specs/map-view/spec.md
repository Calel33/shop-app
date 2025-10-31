## ADDED Requirements

### Requirement: Dedicated Map View
The system SHALL provide a dedicated Map View with Mapbox clustering synchronized with the list query.

#### Scenario: Sync list ↔ map
- **WHEN** a visitor switches to Map View with an active query
- **THEN** map pins and the list pane reflect the same results; pin hover highlights the list item and vice versa

### Requirement: Lazy-load Mapbox
The system MUST lazy-load Mapbox only on the dedicated Map View route to minimize bundle size.

#### Scenario: Mapbox loads on demand
- **WHEN** a visitor navigates to Map View
- **THEN** Mapbox assets load; leaving the view unloads them from active memory where possible

### Requirement: Feature Flag for Live Map
The live Mapbox integration SHALL be gated behind a feature flag until UI is validated with mock data.

#### Scenario: Flag off
- **WHEN** the feature flag is disabled
- **THEN** the Map View renders mock data without calling Mapbox APIs
