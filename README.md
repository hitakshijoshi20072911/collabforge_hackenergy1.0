# CollabForge - Hackathons & Innovation Hub

![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=for-the-badge&logo=typescript)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-CSS-06B6D4?style=for-the-badge&logo=tailwindcss)
![Vite](https://img.shields.io/badge/Vite-Build_Tool-646CFF?style=for-the-badge&logo=vite)
![Accessibility](https://img.shields.io/badge/WCAG-AA_Compliant-success?style=for-the-badge)
![Real Time](https://img.shields.io/badge/Real--Time-Collaboration-blueviolet?style=for-the-badge)

A comprehensive, accessible, and cinematic web application for organizing and participating in hackathons and innovation challenges. Built with React, TypeScript, Tailwind CSS, and designed with WCAG accessibility standards in mind.

##  Features

### For Participants
- **Browse Events**: Discover hackathons with advanced search and filtering
- **Team Management**: Create and join teams, collaborate in real-time
- **Project Submission**: Submit projects with rich media and documentation
- **Dashboard**: Track progress, deadlines, and team activities

### For Judges
- **Submission Queue**: Review projects with keyboard navigation
- **Rubric-Based Scoring**: Evaluate submissions using customizable criteria
- **Feedback System**: Provide constructive feedback to teams

### For Admins
- **Event Creation**: Build events with tracks, prizes, and rules
- **Judge Management**: Assign judges and balance workload
- **Analytics**: Monitor engagement and participant metrics
- **Announcements**: Communicate with participants

##  Design System

### Visual Theme
- **Glassmorphism**: Frosted glass cards with backdrop blur
- **Neon Accents**: Electric blue (#0ea5e9) and cyan (#06b6d4)
- **Dark Background**: Deep indigo (#0f172a) with subtle gradients
- **Smooth Animations**: Respects `prefers-reduced-motion`

### Accessibility
- WCAG AA compliant
- Semantic HTML landmarks
- ARIA labels on all interactive elements
- Keyboard navigation support
- Focus visible states
- Skip to main content link
- Accessibility toolbar (high contrast, reduce motion, larger text)

##  Getting Started

### Prerequisites
- Node.js 18+ and npm

### Installation

```bash
# Clone the repository
git clone <YOUR_GIT_URL>

# Navigate to project directory
cd collabforge

# Install dependencies
npm install

# Start development server
npm run dev
```

The app will be available at `http://localhost:8080`

### Build for Production

```bash
npm run build
```

## 📁 Project Structure

```
src/
├── assets/              # Images and static assets
├── components/
│   ├── ui/             # Reusable UI components (shadcn)
│   ├── layout/         # Layout components (Navbar, Footer)
│   └── events/         # Event-specific components
├── pages/              # Page components
├── lib/                # Utilities (motion, API client)
├── mocks/              # Mock data for demo
├── services/           # API service layer
├── types/              # TypeScript type definitions
└── hooks/              # Custom React hooks
```

## 🔌 Backend Integration

This frontend is ready to connect to a backend API. To integrate:

### 1. Environment Setup

Create a `.env` file:

```env
VITE_API_URL=http://localhost:3000/api
```

### 2. API Endpoints to Implement

All API contracts are defined in `src/services/api.ts`:

#### Authentication
- `POST /api/auth/signup` - User registration
- `POST /api/auth/login` - User login
- `GET /api/auth/me` - Get current user

#### Events
- `GET /api/events` - List events (with filters)
- `GET /api/events/:id` - Event details
- `POST /api/events` - Create event (admin)
- `PUT /api/events/:id` - Update event (admin)

#### Teams
- `POST /api/events/:id/teams` - Create team
- `GET /api/events/:id/teams/:teamId` - Team details
- `POST /api/events/:id/teams/:teamId/join` - Join team

#### Submissions
- `POST /api/events/:id/teams/:teamId/submission` - Submit project
- `GET /api/events/:id/submissions` - List submissions

#### Scoring
- `POST /api/submissions/:id/score` - Submit score (judge)
- `GET /api/submissions/:id/scores` - Get scores

#### File Upload
- `POST /api/uploads/presign` - Get presigned S3 URL
- Client uploads directly to S3 using presigned URL

### 3. WebSocket Events

For real-time features, implement WebSocket at `/ws`:

- `submission:scored` - When a judge scores a submission
- `scoreboard:update` - Scoreboard changes
- `chat:message` - Team chat messages

### 4. Replace Mock Data

1. Update `src/services/api.ts` - uncomment API calls
2. Remove mock implementations
3. Test each endpoint

##  Role-Based Access

The app supports three roles:

- **Participant**: Join events, create teams, submit projects
- **Judge**: Evaluate submissions, provide feedback
- **Admin**: Create events, manage judges, view analytics

### Demo Mode

Use the Auth page to quickly switch between roles for testing.

##  Testing

### Accessibility Testing

```bash
# Install axe-core
npm install --save-dev @axe-core/react

# Run accessibility audit
npm run test:a11y
```

### Keyboard Navigation

Test major flows using only keyboard:
- Tab through all interactive elements
- Use arrow keys in dropdowns
- Press Enter/Space to activate buttons
- Navigate forms with Tab and Shift+Tab

##  Deployment

### Frontend (Vercel/Netlify)

1. Connect your Git repository
2. Configure build settings:
   - Build command: `npm run build`
   - Output directory: `dist`
3. Add environment variables

### Backend (Render/Railway/AWS)

1. Deploy API server
2. Configure database (PostgreSQL)
3. Set up S3 bucket for file storage
4. Configure CORS to allow frontend domain
5. Set environment variables:
   - `DATABASE_URL`
   - `JWT_SECRET`
   - `S3_BUCKET`, `S3_REGION`, `S3_ACCESS_KEY`, `S3_SECRET_KEY`
   - `SENDGRID_API_KEY` (for emails)

##  Key Technologies

- **React 18** - UI framework
- **TypeScript** - Type safety
- **Tailwind CSS** - Styling
- **Vite** - Build tool
- **React Router** - Navigation
- **React Query** - Server state management
- **shadcn/ui** - UI components
- **Lucide React** - Icons
- **date-fns** - Date formatting
- **Axios** - HTTP client

##  Design Tokens

All design tokens are defined in `src/index.css`:

```css
/* Colors */
--primary: 199 89% 48%;        /* Electric blue */
--accent: 187 85% 53%;          /* Neon cyan */
--secondary: 270 60% 50%;       /* Purple */

/* Gradients */
--gradient-primary: linear-gradient(...);
--gradient-accent: linear-gradient(...);

/* Shadows */
--shadow-glow: 0 0 20px hsl(...);

/* Animation */
--duration-fast: 150ms;
--duration-normal: 250ms;
```

##  Security Considerations

### Production Checklist
- [ ] Enable HTTPS
- [ ] Configure secure CORS
- [ ] Implement rate limiting
- [ ] Validate file uploads (type, size)
- [ ] Use parameterized queries (prevent SQL injection)
- [ ] Hash passwords with bcrypt
- [ ] Store JWT securely (httpOnly cookies)
- [ ] Implement CSRF protection
- [ ] Set security headers


---

Built with ❤️ by the CollabForge team
