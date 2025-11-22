# Daily Planner App

A Sunsama-inspired daily planning application built with React and Firebase. This app helps users plan their day, manage tasks, track time, and maintain productivity through structured daily rituals.

## 🎯 Project Overview

This project aims to replicate the core functionality and user experience of Sunsama, a popular daily planning tool, while providing an open-source alternative powered by modern web technologies.

### Inspiration

Based on the Sunsama daily planning workflow, which emphasizes:
- Intentional daily planning
- Time-boxed task management  
- Calendar integration
- Focus mode for deep work
- Daily shutdown rituals

## ✨ Features

### Core Functionality
- **Daily Planning Flow**: Guided 6-step onboarding and daily planning ritual
- **Task Management**: Create, organize, and track tasks with subtasks
- **Time Tracking**: Built-in timer with actual vs. planned time comparison
- **Calendar Integration**: Visual timeline with drag-and-drop scheduling
- **Focus Mode**: Distraction-free view for working on individual tasks
- **Multi-day View**: See today, tomorrow, and upcoming days side-by-side
- **Tags & Categories**: Organize tasks with customizable tags
- **Daily Rituals**: Morning planning and evening shutdown routines

### UI/UX Features
- Clean, minimal interface with generous whitespace
- Responsive design for desktop and mobile
- Keyboard shortcuts for power users
- Progress indicators and visual feedback
- Smooth animations and transitions

## 🏗️ Tech Stack

### Frontend
- **React 18+**: Modern React with hooks and functional components
- **React Router**: Client-side routing
- **Tailwind CSS**: Utility-first CSS framework for styling
- **Date-fns**: Date manipulation and formatting
- **React DnD**: Drag-and-drop functionality
- **Framer Motion**: Smooth animations

### Backend & Infrastructure
- **Firebase Authentication**: User auth with email/password and social logins
- **Firebase Firestore**: Real-time NoSQL database
- **Firebase Functions**: Serverless backend logic
- **Firebase Hosting**: Fast, secure web hosting
- **Firebase Storage**: File storage for user uploads

### Development Tools
- **Vite**: Next-generation frontend build tool
- **ESLint**: Code linting
- **Prettier**: Code formatting
- **Husky**: Git hooks

## 📋 Product Requirements Document

### User Stories

#### As a user, I want to:
1. **Plan my day** through a guided workflow that helps me:
   - Add tasks I want to work on
   - Estimate time for each task
   - Pull in tasks from integrated tools
   - Prioritize my task list
   - Schedule tasks on my calendar
   - Document my plan and share it

2. **Manage tasks** with the ability to:
   - Create tasks with titles and descriptions
   - Add subtasks to break down work
   - Set time estimates
   - Assign tags/categories
   - Mark tasks as complete
   - Reschedule incomplete tasks

3. **Track my time** by:
   - Starting/stopping timers on tasks
   - Seeing actual vs. planned time
   - Getting notifications when time is up
   - Reviewing time spent at end of day

4. **Focus on one task** with:
   - Distraction-free focus mode
   - Visible timer countdown
   - Subtask checklist
   - Quick access to task notes

5. **View my schedule** through:
   - Multi-day calendar view
   - Time-blocked tasks
   - Scheduled events from external calendars
   - Easy drag-and-drop rescheduling

### Technical Requirements

#### Authentication
- Email/password registration and login
- Google OAuth integration
- Password reset functionality
- Session management with Firebase Auth

#### Data Models

**User**
```javascript
{
  uid: string,
  email: string,
  displayName: string,
  photoURL: string,
  settings: {
    workStartTime: string, // e.g., "9:00 AM"
    workEndTime: string,   // e.g., "5:00 PM"
    planningTime: string,  // "start" or "night_before"
    theme: string,         // "light" or "dark"
  },
  createdAt: timestamp,
  updatedAt: timestamp
}
```

**Task**
```javascript
{
  id: string,
  userId: string,
  title: string,
  description: string,
  scheduledDate: date,
  scheduledTime: string,
  plannedDuration: number, // minutes
  actualDuration: number,  // minutes
  status: string,          // "todo", "in_progress", "completed"
  tags: [string],
  subtasks: [{
    id: string,
    title: string,
    completed: boolean,
    actualDuration: number
  }],
  timerStartedAt: timestamp | null,
  completedAt: timestamp | null,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

**Daily Plan**
```javascript
{
  id: string,
  userId: string,
  date: date,
  taskIds: [string],
  notes: string,
  obstacles: string,
  totalPlannedTime: number,
  completedAt: timestamp | null,
  createdAt: timestamp
}
```

#### API Endpoints (Firebase Functions)

- `POST /api/tasks` - Create a new task
- `GET /api/tasks` - Get all tasks for user
- `GET /api/tasks/:id` - Get specific task
- `PUT /api/tasks/:id` - Update task
- `DELETE /api/tasks/:id` - Delete task
- `POST /api/tasks/:id/start-timer` - Start task timer
- `POST /api/tasks/:id/stop-timer` - Stop task timer
- `POST /api/daily-plans` - Create daily plan
- `GET /api/daily-plans/:date` - Get plan for specific date
- `PUT /api/user/settings` - Update user settings

### UI Components

#### Onboarding Flow
1. **Welcome Screen** - Introduction to daily planning
2. **Step 1: Add Task** - Simple input form
3. **Step 2: Time Estimation** - Time slider/input
4. **Step 3: Fill Task List** - Calendar integration view
5. **Step 4: Prioritize** - Drag-and-drop reordering
6. **Step 5: Schedule** - Calendar time-blocking
7. **Step 6: Document** - Summary and sharing

#### Main Dashboard
- **Sidebar Navigation**
  - Home
  - Today
  - Focus Mode
  - Daily Rituals (Planning, Shutdown, Highlights)
  - Weekly Rituals (Planning, Review)
  - Settings

- **Top Bar**
  - Date selector
  - Filter options
  - Board/Calendar view toggle
  - User menu

- **Main Content**
  - Three-column day view (Yesterday/Today/Tomorrow)
  - Task cards with drag-and-drop
  - Quick add task button
  - Progress indicators

- **Right Panel (Calendar)**
  - Hour-by-hour timeline
  - Color-coded task blocks
  - External calendar events
  - Quick rescheduling

#### Focus Mode
- Large task title
- Timer display (actual vs. planned)
- Start/Stop button
- Subtask checklist
- Notes area
- Exit to dashboard button

### Performance Requirements
- Initial page load < 2 seconds
- Task operations < 200ms
- Real-time updates < 500ms
- Offline capability with sync
- Support 1000+ tasks per user

### Security Requirements
- All API requests authenticated
- Firestore security rules enforce user data isolation
- Input validation and sanitization
- HTTPS only
- Regular security audits

## 🚀 Getting Started

### Prerequisites
- Node.js 18+ and npm
- Firebase account
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/ChrisCruze/daily-planner-app.git
cd daily-planner-app

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your Firebase config

# Start development server
npm run dev
```

### Firebase Setup

1. Create a new Firebase project at https://console.firebase.google.com/
2. Enable Authentication (Email/Password and Google)
3. Create a Firestore database
4. Copy your Firebase config to `.env`
5. Deploy security rules:
```bash
firebase deploy --only firestore:rules
```

## 📁 Project Structure

```
daily-planner-app/
├── src/
│   ├── components/       # Reusable UI components
│   │   ├── common/       # Buttons, inputs, modals
│   │   ├── tasks/        # Task cards, lists
│   │   ├── calendar/     # Calendar views
│   │   └── onboarding/   # Onboarding steps
│   ├── pages/            # Route pages
│   │   ├── Home.jsx
│   │   ├── Today.jsx
│   │   ├── Focus.jsx
│   │   └── Settings.jsx
│   ├── hooks/            # Custom React hooks
│   ├── contexts/         # React contexts
│   ├── services/         # Firebase services
│   ├── utils/            # Utility functions
│   ├── styles/           # Global styles
│   └── App.jsx           # Main app component
├── functions/            # Firebase Cloud Functions
├── firestore.rules       # Firestore security rules
├── firebase.json         # Firebase configuration
└── package.json
```

## 🎨 Design System

### Colors
- Primary Green: `#10B981` (Emerald-500)
- Text Dark: `#2D3748`
- Text Medium: `#718096`
- Text Light: `#9CA3AF`
- Background: `#FAFBFC`
- Border: `#E2E8F0`
- Orange Tag: `#F59E0B`

### Typography
- Font Family: Inter, system-ui, sans-serif
- Headings: 18-32px, weight 600-700
- Body: 14-16px, weight 400
- Small: 12-13px, weight 400

### Spacing
- Base unit: 4px
- Common: 8px, 12px, 16px, 20px, 24px, 32px

## 🧪 Testing

```bash
# Run unit tests
npm test

# Run e2e tests
npm run test:e2e

# Generate coverage report
npm run test:coverage
```

## 📦 Deployment

```bash
# Build for production
npm run build

# Deploy to Firebase Hosting
firebase deploy
```

## 🗺️ Roadmap

### Phase 1: MVP (Current)
- [x] Basic task management
- [x] Daily planning flow
- [x] Focus mode
- [x] Time tracking
- [ ] Calendar integration

### Phase 2: Integrations
- [ ] Google Calendar sync
- [ ] Todoist integration
- [ ] Gmail integration
- [ ] Slack integration

### Phase 3: Collaboration
- [ ] Team workspaces
- [ ] Shared tasks
- [ ] Team rituals
- [ ] Activity feed

### Phase 4: Mobile
- [ ] React Native mobile app
- [ ] Offline-first sync
- [ ] Push notifications

## 🤝 Contributing

Contributions are welcome! Please read our contributing guidelines and code of conduct.

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## 📄 License

MIT License - see LICENSE file for details

## 🙏 Acknowledgments

- Inspired by [Sunsama](https://sunsama.com/)
- UI patterns from modern productivity tools
- Firebase for backend infrastructure

## 📞 Contact

For questions or feedback, please open an issue on GitHub.

---

**Built with ❤️ for better productivity**
