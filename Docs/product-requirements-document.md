# Product Requirements Document: theAGNT.ai

## Executive Summary

theAGNT.ai is a stealth-mode portfolio company website designed to build mystique and collect early-access interest for our AI-led ventures. The site serves as a minimalist gateway that captures qualified leads while revealing nothing about our specific ventures or capabilities.

## Product Vision

Create an enigmatic digital presence that:
- Generates curiosity through sophisticated minimalism
- Filters for high-intent early adopters
- Maintains complete operational secrecy
- Builds a qualified waitlist for future venture launches

## Core Requirements

### 1. Authentication System

**Requirement**: Multi-provider authentication
- **Providers**: Email (magic link), Google OAuth, Apple Sign-in
- **User Data Captured**: Email, name (if provided), auth provider, signup timestamp
- **Security**: Industry-standard OAuth 2.0, secure token management
- **Session Management**: Persistent sessions with secure refresh tokens

### 2. User Journey

**Public Landing Page**
- Single-page experience with brand mark
- Minimal copy: Just "theAGNT.ai" and authentication options
- No explanation of what we do
- Dark, sophisticated aesthetic

**Authenticated Experience**
- **State 1 - Not on Waitlist**: 
  - Centered button: "Join the Waitlist"
  - No additional context or explanation
  - Single-click action
  
- **State 2 - On Waitlist**:
  - Centered text: "You're on the waitlist."
  - Subtle animation or visual feedback
  - No position number or timeline

### 3. Data Model

**Users Table**
- `id`: UUID primary key
- `email`: Unique, required
- `name`: Optional from OAuth
- `auth_provider`: enum (email, google, apple)
- `created_at`: Timestamp
- `last_login`: Timestamp

**Waitlist Table**
- `id`: UUID primary key
- `user_id`: Foreign key to users
- `joined_at`: Timestamp
- `metadata`: JSONB for future use

### 4. Admin Dashboard

**Access Control**
- Restricted to darrenapfel@gmail.com only
- Accessible at /admin route
- Additional authentication layer

**Dashboard Features**
- Total signups count
- Waitlist conversion rate
- User table with:
  - Email
  - Sign-up date/time
  - Auth provider
  - Waitlist status
  - Last login
- Export functionality (CSV)
- Basic filtering and search

## Non-Functional Requirements

### Performance
- Page load < 1 second
- Time to interactive < 2 seconds
- Lighthouse score > 95

### Security
- All data encrypted at rest
- HTTPS only
- Rate limiting on auth endpoints
- GDPR compliant data handling

### Scalability
- Support 100,000+ waitlist signups
- Handle viral traffic spikes
- Zero downtime deployments

### Analytics
- Privacy-first analytics (no personal data)
- Track: Page views, sign-ups, waitlist conversions
- A/B testing capability for future iterations

## Success Metrics

1. **Conversion Rate**: Landing → Sign-up (target: >15%)
2. **Waitlist Conversion**: Sign-up → Waitlist (target: >60%)
3. **Return Rate**: Users checking status (indicates interest)
4. **Time on Site**: Brief by design (<30 seconds expected)

## Technical Constraints

- Must use our standard stack (Next.js, TypeScript, Tailwind, Supabase)
- Mobile-first responsive design
- Progressive enhancement
- Works without JavaScript (auth fallback)

## Future Considerations

- Referral system for waitlist members
- Selective reveal of ventures to waitlist
- Tiered access (VIP waitlist)
- Integration with future venture launches

## Out of Scope

- Content/blog
- About page or team info
- Social media links
- Contact information
- Any explanation of services
- Venture portfolio display

## Launch Requirements

1. Custom domain setup (theAGNT.ai)
2. SSL certificate
3. Monitoring and alerting
4. Backup strategy
5. GDPR/privacy policy (minimal)

## Timeline

This is a high-priority project to establish our digital presence before venture launches. Target: Complete MVP within 7 days.