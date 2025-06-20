# Architecture Document: theAGNT.ai

## System Overview

theAGNT.ai is a minimalist web application built on our standard Claude-first tech stack. The architecture prioritizes simplicity, security, and scalability while maintaining the mysterious aesthetic defined in our design requirements.

## Tech Stack

### Frontend
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript (strict mode)
- **Styling**: Tailwind CSS + CSS Modules
- **Authentication**: NextAuth.js v5
- **State Management**: React Context (minimal needs)
- **Animation**: Framer Motion (selective use)

### Backend
- **Database**: Supabase (PostgreSQL)
- **Authentication**: Supabase Auth (integrated with NextAuth)
- **API**: Next.js API Routes
- **Edge Functions**: Supabase Edge Functions (if needed)
- **File Storage**: Supabase Storage (future use)

### Infrastructure
- **Hosting**: Vercel (frontend)
- **Database**: Supabase Cloud
- **Domain**: theAGNT.ai (via Vercel)
- **CDN**: Vercel Edge Network
- **Analytics**: Vercel Analytics (privacy-first)

### Development
- **Version Control**: Git/GitHub
- **CI/CD**: Vercel automatic deployments
- **Testing**: Jest + React Testing Library + Playwright
- **Linting**: ESLint + Prettier
- **Package Manager**: npm

## Database Schema

```sql
-- Users table (managed by Supabase Auth)
-- Automatically created, includes:
-- id, email, created_at, updated_at, etc.

-- Waitlist table
CREATE TABLE waitlist (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id UUID REFERENCES auth.users(id) ON DELETE CASCADE,
  joined_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  metadata JSONB DEFAULT '{}',
  UNIQUE(user_id)
);

-- Create RLS policies
ALTER TABLE waitlist ENABLE ROW LEVEL SECURITY;

-- Users can only see their own waitlist status
CREATE POLICY "Users can view own waitlist status" ON waitlist
  FOR SELECT USING (auth.uid() = user_id);

-- Users can join waitlist
CREATE POLICY "Users can join waitlist" ON waitlist
  FOR INSERT WITH CHECK (auth.uid() = user_id);

-- Admin view (for dashboard)
CREATE POLICY "Admin full access" ON waitlist
  FOR ALL USING (auth.jwt() ->> 'email' = 'darrenapfel@gmail.com');
```

## Application Architecture

### Directory Structure
```
theagnt-website/
├── app/
│   ├── layout.tsx          # Root layout with providers
│   ├── page.tsx            # Landing page
│   ├── auth/
│   │   ├── signin/page.tsx # Sign in page (if needed)
│   │   └── error/page.tsx  # Auth error handling
│   ├── dashboard/
│   │   └── page.tsx        # Authenticated user view
│   ├── admin/
│   │   ├── layout.tsx      # Admin layout with extra auth
│   │   └── page.tsx        # Admin dashboard
│   └── api/
│       ├── auth/[...nextauth]/route.ts
│       └── waitlist/route.ts
├── components/
│   ├── auth/
│   │   ├── AuthButton.tsx
│   │   └── AuthProvider.tsx
│   ├── waitlist/
│   │   ├── JoinButton.tsx
│   │   └── WaitlistStatus.tsx
│   └── ui/
│       └── Logo.tsx
├── lib/
│   ├── auth.ts             # NextAuth configuration
│   ├── supabase.ts         # Supabase client
│   └── utils.ts
├── styles/
│   └── globals.css         # Minimal global styles
├── types/
│   └── index.ts            # TypeScript types
└── middleware.ts           # Auth middleware
```

### Authentication Flow

1. **Landing Page** → User clicks auth provider
2. **OAuth Flow** → Redirect to provider (Google/Apple)
3. **Callback** → Provider returns to `/api/auth/callback`
4. **Session Creation** → NextAuth creates session
5. **User Sync** → Sync with Supabase auth.users
6. **Redirect** → Send to `/dashboard`

### Key Components

#### AuthProvider
```typescript
// Wraps app with NextAuth session provider
// Handles session state and refresh
```

#### WaitlistManager
```typescript
// Checks user's waitlist status
// Handles join waitlist action
// Updates UI based on status
```

#### AdminGuard
```typescript
// Middleware component for admin routes
// Verifies email === 'darrenapfel@gmail.com'
// Redirects unauthorized users
```

## Security Architecture

### Authentication Security
- OAuth 2.0 for Google/Apple
- Magic links for email (no passwords)
- Secure session tokens (httpOnly cookies)
- CSRF protection built-in

### Data Security
- All data encrypted at rest (Supabase)
- TLS 1.3 for all connections
- Row Level Security (RLS) policies
- No client-side data exposure

### API Security
- Rate limiting on all endpoints
- Input validation with Zod
- SQL injection prevention (parameterized queries)
- XSS protection (React default)

## Performance Optimization

### Frontend Performance
- Static generation for landing page
- Dynamic imports for auth providers
- Image optimization (none needed currently)
- Font optimization (Inter subset)
- Minimal JavaScript bundle

### Database Performance
- Indexed on user_id for fast lookups
- Connection pooling via Supabase
- Prepared statements for common queries
- Minimal data transfer

### Caching Strategy
- Static assets: 1 year cache
- API responses: No cache (real-time data)
- Session data: In-memory + cookie

## Monitoring & Observability

### Application Monitoring
- Vercel Analytics for performance
- Error tracking with Vercel
- Uptime monitoring via Vercel

### Database Monitoring
- Supabase dashboard metrics
- Query performance tracking
- Connection pool monitoring

### Logging
- Structured logging with timestamps
- Error logs for failed auth attempts
- Admin action audit trail

## Deployment Architecture

### Environments
1. **Development**: Local Next.js dev server
2. **Preview**: Vercel preview deployments
3. **Production**: theAGNT.ai domain

### CI/CD Pipeline
```yaml
1. Push to GitHub
2. Vercel webhook triggered
3. Build and type check
4. Run tests
5. Deploy to preview
6. Manual promotion to production
```

### Environment Variables
```env
# Public (exposed to client)
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=

# Server-only
NEXTAUTH_URL=
NEXTAUTH_SECRET=
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
APPLE_CLIENT_ID=
APPLE_CLIENT_SECRET=
SUPABASE_SERVICE_KEY=
```

## Scalability Considerations

### Horizontal Scaling
- Vercel automatically scales Next.js
- Supabase handles database scaling
- Stateless architecture enables infinite frontend nodes

### Vertical Scaling
- Database: Auto-scaling with Supabase
- API: Serverless functions scale automatically
- CDN: Global edge network distribution

### Future Scaling Needs
- Redis for session management (if needed)
- Queue system for batch operations
- Read replicas for reporting

## Development Workflow

### Local Development
```bash
# Install dependencies
npm install

# Set up environment variables
cp .env.example .env.local

# Run development server
npm run dev

# Run tests
npm test
npm run test:e2e
```

### Testing Strategy
- Unit tests for utilities and hooks
- Integration tests for API routes
- E2E tests for critical user flows
- Visual regression tests for UI

### Code Quality
```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint",
    "type-check": "tsc --noEmit",
    "test": "jest",
    "test:e2e": "playwright test",
    "format": "prettier --write .",
    "validate": "npm run type-check && npm run lint && npm run test"
  }
}
```

## Integration Points

### Current Integrations
1. **Supabase Auth**: User management
2. **OAuth Providers**: Google, Apple
3. **Vercel Analytics**: Usage tracking

### Future Integrations
1. **Email Service**: Waitlist notifications
2. **CRM**: User relationship management
3. **Venture Platforms**: Launch integrations

## Disaster Recovery

### Backup Strategy
- Database: Automated daily backups (Supabase)
- Code: Git repository (GitHub)
- Secrets: Secure backup in password manager

### Recovery Procedures
1. Database failure: Restore from Supabase backup
2. Frontend failure: Rollback Vercel deployment
3. Auth failure: Fallback to email magic links

## Cost Analysis

### Monthly Costs
- Vercel Pro: $20 (after credits)
- Supabase Free Tier: $0 (up to 500MB)
- Domain: ~$15/year ($1.25/month)
- **Total**: ~$21.25/month

### Scaling Costs
- 10K users: ~$25/month
- 100K users: ~$135/month
- 1M users: ~$400/month

## Success Metrics

### Technical KPIs
- Page load time < 1s
- Lighthouse score > 95
- Zero downtime deployments
- API response time < 200ms

### Business KPIs
- Sign-up conversion rate
- Waitlist join rate
- Admin dashboard usage
- User retention (return visits)

## Timeline

### Phase 1: Foundation (Days 1-2)
- Project setup
- Authentication implementation
- Database schema

### Phase 2: Core Features (Days 3-4)
- Landing page
- Waitlist functionality
- Admin dashboard

### Phase 3: Polish (Days 5-6)
- Animations and transitions
- Testing suite
- Performance optimization

### Phase 4: Launch (Day 7)
- Domain configuration
- Production deployment
- Monitoring setup

This architecture provides a solid foundation for theAGNT.ai while maintaining flexibility for future venture integrations.