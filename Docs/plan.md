# theAGNT.ai Autonomous Development Plan

## Project Status: READY TO START
**Location**: `/Users/darrenapfel/DEVELOPER/CatalystWeb/catalyst-web/`
**GitHub Repo**: https://github.com/darrenapfel/catalyst-web
**Timeline**: 7 days autonomous development
**Permissions**: Updated and ready for autonomous development

## Project Overview
Building theAGNT.ai - a mysterious, minimalist portfolio website with:
- Multi-provider authentication (Google, Apple, Email)
- Waitlist functionality 
- Admin dashboard (restricted to darrenapfel@gmail.com)
- Dark minimalist design with sophisticated animations
- Complete stealth-mode aesthetic (no explanations anywhere)

## Key Requirements Summary
- **Tech Stack**: Next.js 14, TypeScript, Tailwind CSS, Supabase, NextAuth.js
- **Design**: Pure dark theme, minimalist, mysterious
- **Performance**: Lighthouse >95, <1s load time
- **Security**: OAuth 2.0, RLS policies, encrypted data
- **Admin**: Full dashboard with user metrics and CSV export

## Development Phases

### Phase 1: Foundation Setup (Day 1)
- [x] GitHub repo created: https://github.com/darrenapfel/catalyst-web
- [ ] **NEXT: Initialize Next.js 14 project with TypeScript**
- [ ] Configure Tailwind CSS with custom design tokens from design doc
- [ ] Set up ESLint, Prettier, Jest, Playwright
- [ ] Install dependencies: NextAuth.js, Supabase client, Framer Motion
- [ ] Create project structure as defined in architecture doc

### Phase 2: Supabase Backend (Day 1-2)
- [ ] **Create Supabase project via MCP tools**
- [ ] Set up database schema:
  ```sql
  CREATE TABLE waitlist (
    id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
    user_id UUID REFERENCES auth.users(id) ON DELETE CASCADE,
    joined_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    metadata JSONB DEFAULT '{}',
    UNIQUE(user_id)
  );
  ```
- [ ] Configure RLS policies for security
- [ ] Set up authentication providers (Google, Apple, Email magic link)
- [ ] Test database connectivity and auth flow

### Phase 3: Authentication System (Day 2-3)
- [ ] Configure NextAuth.js with all providers
- [ ] Create auth middleware for protected routes
- [ ] Build user sync between NextAuth and Supabase
- [ ] Implement session management
- [ ] Create admin route protection (darrenapfel@gmail.com only)

### Phase 4: Frontend Implementation (Day 3-4)
- [ ] **Landing Page**:
  - Black background with "theAGNT.ai" logo
  - Breathing animation (opacity 1 → 0.8 → 1, 4s loop)
  - Three auth buttons: Google, Apple, Email
  - Hover states and micro-interactions
  
- [ ] **Authenticated Dashboard**:
  - State 1: "Join the Waitlist" button (centered, 200px × 56px)
  - State 2: "You're on the waitlist." confirmation (#00FF88 color)
  - Smooth state transitions
  
- [ ] **Admin Dashboard**:
  - User metrics and analytics
  - Data table with email, signup date, auth provider, waitlist status
  - CSV export functionality
  - Brutalist design aesthetic

### Phase 5: Styling & Animations (Day 4-5)
- [ ] Implement design system:
  - Colors: #000000, #0A0A0A, #FFFFFF, #1A1A1A, #2A2A2A, #00FF88
  - Typography: Inter (200 for logo, 400 for body, 500 for buttons)
  - Spacing: 8px base unit system
  
- [ ] Add micro-interactions:
  - Page fade-in from black (0.5s)
  - Button hover effects (200ms ease-out)
  - Loading states with spinners
  - Waitlist confirmation animation
  
- [ ] Mobile responsiveness across all breakpoints
- [ ] Accessibility compliance (WCAG AA)

### Phase 6: API Routes & Logic (Day 5-6)
- [ ] `/api/auth/[...nextauth]/route.ts` - Authentication handling
- [ ] `/api/waitlist/route.ts` - Waitlist join/status endpoints
- [ ] `/api/admin/route.ts` - Admin dashboard data endpoints
- [ ] Input validation with Zod
- [ ] Error handling and rate limiting
- [ ] Database query optimization

### Phase 7: Testing Suite (Day 6)
- [ ] **Unit Tests**:
  - Authentication utilities
  - Waitlist management functions
  - Component rendering tests
  
- [ ] **Integration Tests**:
  - API route testing
  - Database operations
  - Auth flow testing
  
- [ ] **E2E Tests** (Playwright):
  - Complete user signup flow
  - Waitlist join flow
  - Admin dashboard access
  - Cross-browser testing

### Phase 8: Performance & Optimization (Day 6-7)
- [ ] Bundle analysis and optimization
- [ ] Font loading optimization (Inter subset)
- [ ] Image optimization (SVG logos only)
- [ ] Implement caching strategies
- [ ] Achieve Lighthouse score >95
- [ ] Performance monitoring setup

### Phase 9: Production Build & Local Deployment (Day 7)
- [ ] Configure environment variables
- [ ] Run complete validation suite
- [ ] Build production optimized version
- [ ] Set up local production server
- [ ] Configure error monitoring
- [ ] Test all functionality in production mode

## Required Environment Variables
```env
# Public
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=

# Server-only  
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
APPLE_CLIENT_ID=
APPLE_CLIENT_SECRET=
SUPABASE_SERVICE_KEY=
```

## Package.json Scripts Required
```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build", 
    "start": "next start",
    "lint": "next lint",
    "type-check": "tsc --noEmit",
    "test": "jest --watch",
    "test:ci": "jest --ci",
    "test:e2e": "playwright test",
    "test:e2e:ui": "playwright test --ui",
    "format": "prettier --write .",
    "format:check": "prettier --check .",
    "validate": "npm run type-check && npm run lint && npm run format:check && npm run test:ci",
    "validate:full": "npm run validate && npm run test:e2e"
  }
}
```

## Success Criteria Checklist
- [ ] All authentication providers working
- [ ] Waitlist functionality fully operational  
- [ ] Admin dashboard accessible and functional
- [ ] Dark theme design perfectly implemented
- [ ] All animations and micro-interactions working
- [ ] Mobile responsive across all devices
- [ ] Lighthouse score >95 achieved
- [ ] All tests passing (unit + integration + e2e)
- [ ] Production build successful
- [ ] Local deployment running smoothly
- [ ] Ready for theAGNT.ai domain deployment

## Important Notes
- **Design Philosophy**: No explanatory text anywhere, maintain complete mystery
- **Admin Access**: Only darrenapfel@gmail.com can access /admin
- **Performance**: <1s page load, <2s time to interactive
- **Security**: All data encrypted, RLS policies enforced
- **Aesthetic**: Sophisticated minimalism, whispers power through absence

## MCP Tools Available
- Supabase MCP: Full backend automation
- Context7 MCP: Live documentation lookup
- GitHub MCP: Repository management

## File Locations Reference
- **Project Root**: `/Users/darrenapfel/DEVELOPER/CatalystWeb/catalyst-web/`
- **Docs**: `/Users/darrenapfel/DEVELOPER/CatalystWeb/catalyst-web/Docs/`
- **Requirements**: `product-requirements-document.md`
- **Design**: `design-document.md` 
- **Architecture**: `architecture-document.md`

---

**AUTONOMOUS DEVELOPMENT STATUS**: Ready to begin Phase 1 after restart.
**NEXT ACTION**: Initialize Next.js 14 project with TypeScript and begin foundation setup.