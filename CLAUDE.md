# CLAUDE.md - Project Instructions for AI Assistant

## Project Overview

**Project Name**: DemoAssist
**Purpose**: Elderly care management system (SEPAW - likely "ระบบดูแลผู้สูงอายุ")
**Tech Stack**: Next.js 14 + TypeScript + PostgreSQL + Prisma

This is a full-stack web application for managing elderly care services, including caregivers, local government officials (อบต.), and administrators.

## Architecture

### Frontend
- **Framework**: Next.js 14 with TypeScript
- **Routing**: Hybrid - uses both `/src/app` (App Router) and `/src/pages` (Pages Router)
- **Styling**: Tailwind CSS + Bootstrap + SASS
- **State Management**: Redux Toolkit
- **Forms**: React Hook Form + Zod validation
- **UI Components**:
  - Charts: Chart.js + react-chartjs-2
  - Calendar: FullCalendar + react-calendar
  - Date Picker: react-datepicker
  - Maps: Google Maps API (@react-google-maps/api)
  - Select: react-select

### Backend
- **API**: Next.js API Routes
- **Database**: PostgreSQL (database name: `sepawv2`)
- **ORM**: Prisma
- **Authentication**: JWT + bcrypt
- **Security**: crypto-js, md5 hashing

### Project Structure
```
src/
├── app/              # App Router pages (Next.js 13+)
├── pages/            # Pages Router (legacy/API routes)
├── components/       # Reusable React components
├── context/          # React Context providers
├── hooks/            # Custom React hooks
├── hoc/              # Higher-Order Components
├── lib/              # Library utilities and configurations
├── redux/            # Redux store, slices, and actions
├── styles/           # Global styles and SASS files
├── types/            # TypeScript type definitions
├── utils/            # Utility functions
└── middleware.ts     # Next.js middleware
```

## Development

### Environment Setup

**Development Port**: 3050 (not default 3000)

**Required Environment Files**:
- `env.development.local` - Development environment variables
- `env.production.local` - Production environment variables

**Database Configuration**:
- Database: PostgreSQL
- Database Name: `sepawv2`
- Default User: `postgres`
- Default Password: `root`

### Common Commands

```bash
# Development
npm run dev              # Start dev server on port 3050

# Build
npm run build           # Production build
npm run start           # Start production server
npm run vercel-build    # Build for Vercel deployment

# Linting
npm run lint            # Run ESLint

# Database (Prisma)
npx prisma migrate dev  # Run migrations in development
npx prisma db push      # Push schema to database
npx prisma generate     # Generate Prisma Client
npx prisma studio       # Open Prisma Studio GUI
```

### Database Schema Key Entities

Based on README.md, the database includes:
- **gender**: Gender options (ชาย, หญิง, ไม่ระบุ)
- **status**: User roles (ผู้ดูแลผู้สูงอายุ, เจ้าหน้าที่ อบต., admin)
- **marrystatus**: Marital status (โสด, สมรส, หย่า/หม้าย, แยกกันอยู่)

## Guidelines for Claude

### Code Modification Rules

1. **Read Before Edit**: Always read files before modifying them
2. **Preserve Thai Language**: This project uses Thai language for UI and data - preserve all Thai text
3. **Authentication**: Be mindful of JWT authentication patterns - check middleware.ts
4. **Database Changes**:
   - Always update Prisma schema for database changes
   - Run `npx prisma generate` after schema updates
   - Create migrations with `npx prisma migrate dev`
5. **Type Safety**: Maintain TypeScript types - check `/src/types` and `types.d.ts`
6. **State Management**: Use Redux for global state - check `/src/redux`

### Common Patterns

- **API Routes**: Located in `/src/pages/api/` or `/src/app/api/`
- **Authentication**: Uses JWT tokens stored in cookies (js-cookie)
- **Form Validation**: Use Zod schemas with react-hook-form
- **Date Handling**: Use moment-timezone for consistent date/time handling
- **Error Handling**: Check existing error handling patterns before adding new ones

### What NOT to Do

- Don't change the dev server port (3050)
- Don't modify database credentials in README.md (they're documentation)
- Don't add comments to code that's already self-explanatory
- Don't over-engineer - keep solutions simple
- Don't modify authentication logic without understanding the full flow
- Don't change Thai language text without user approval

### Security Considerations

- This app handles personal elderly care data - be careful with PII
- Authentication tokens are managed via JWT - don't expose secrets
- Database backup files (`backupafe.sql`, `backupdata3.sql`) exist - don't commit new backups
- Follow OWASP top 10 - watch for SQL injection, XSS, CSRF

### Testing Before Suggesting

When suggesting code changes:
1. Check if the pattern already exists elsewhere in the codebase
2. Verify imports are available in package.json
3. Consider both Thai and English language support
4. Test database queries against the Prisma schema

## Key Dependencies

- **next**: ^14.2.35
- **react**: ^18.3.1
- **@prisma/client**: ^6.1.0
- **@reduxjs/toolkit**: ^2.2.7
- **react-hook-form**: ^7.71.1
- **zod**: ^3.25.76
- **jsonwebtoken**: ^9.0.2
- **bcrypt**: ^5.1.1
- **moment-timezone**: ^0.5.44

## Additional Context

- The project appears to be a government-related system for elderly care management
- It supports multiple user roles: caregivers, local government officials, and administrators
- The system likely tracks elderly individuals, their caregivers, and related services
- Geographic location tracking is enabled via Google Maps integration
- The calendar functionality suggests event/appointment scheduling features

## Questions to Ask Before Major Changes

1. Does this change affect user authentication or authorization?
2. Will this modify database schema? (Need migration?)
3. Does this impact Thai language display or data?
4. Will this change affect multiple user roles differently?
5. Is this a new feature or fixing existing functionality?

---

**Last Updated**: 2026-02-03
**Claude Code Version**: Use this file as primary context for understanding this codebase.
