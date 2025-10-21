# FixBuddy - Project Documentation

## Table of Contents
1. [Project Overview](#project-overview)
2. [Technology Stack](#technology-stack)
3. [Project Structure](#project-structure)
4. [Features Implemented](#features-implemented)
5. [Database Schema](#database-schema)
6. [API Routes](#api-routes)
7. [Authentication System](#authentication-system)
8. [Admin Panel](#admin-panel)
9. [Setup Instructions](#setup-instructions)
10. [Key Components](#key-components)

---

## Project Overview

**FixBuddy** is a community-driven Q&A platform specifically designed for home appliance repairs and troubleshooting. It's similar to Stack Overflow but focused on helping people fix their appliances like refrigerators, washing machines, dishwashers, etc.

### Purpose
The platform allows users to:
- Ask questions about appliance problems
- Provide answers and solutions to help others
- Vote on questions and answers
- Accept best answers
- Comment on questions and answers
- Search and filter by tags
- Build reputation through helpful contributions

---

## Technology Stack

### Frontend
- **Next.js 15.5.6** - React framework with App Router
- **TypeScript** - Type-safe JavaScript
- **Tailwind CSS** - Utility-first CSS framework
- **React** - UI library

### Backend
- **Next.js API Routes** - Serverless API endpoints
- **MongoDB** - NoSQL database
- **Mongoose** - MongoDB object modeling

### Development Tools
- **Turbopack** - Fast bundler for Next.js
- **ESLint** - Code linting
- **TypeScript** - Static type checking

---

## Project Structure

```
fixbuddy/
├── app/                          # Next.js App Router
│   ├── api/                      # API Routes
│   │   ├── admin/               # Admin endpoints
│   │   ├── answers/             # Answer endpoints
│   │   ├── auth/                # Authentication endpoints
│   │   ├── comments/            # Comment endpoints
│   │   ├── questions/           # Question endpoints
│   │   ├── search/              # Search endpoints
│   │   ├── stats/               # Statistics endpoints
│   │   ├── tags/                # Tag endpoints
│   │   └── users/               # User endpoints
│   ├── admin/                   # Admin panel pages
│   ├── ask/                     # Ask question page
│   ├── login/                   # Login page
│   ├── questions/               # Question pages
│   ├── register/                # Registration page
│   ├── search/                  # Search page
│   ├── tags/                    # Tags pages
│   ├── users/                   # User profile pages
│   ├── layout.tsx               # Root layout
│   ├── page.tsx                 # Homepage
│   └── globals.css              # Global styles
├── components/                  # Reusable React components
│   ├── AnswerCard.tsx
│   ├── CommentSection.tsx
│   ├── Navbar.tsx
│   ├── QuestionCard.tsx
│   ├── QuestionForm.tsx
│   ├── VoteButton.tsx
│   └── ... (other components)
├── contexts/                    # React Context providers
│   └── AuthContext.tsx
├── lib/                         # Utility functions and models
│   ├── models/                  # Mongoose models
│   │   ├── User.ts
│   │   ├── Question.ts
│   │   ├── Answer.ts
│   │   ├── Tag.ts
│   │   └── Comment.ts
│   ├── auth.ts                  # Authentication utilities
│   ├── adminAuth.ts             # Admin authentication
│   ├── mongodb.js               # MongoDB connection
│   └── apiResponse.ts           # API response helpers
├── scripts/                     # Utility scripts
│   └── seed.ts                  # Database seeding script
├── types/                       # TypeScript type definitions
│   └── api.ts
└── package.json                 # Project dependencies
```

---

## Features Implemented

### 1. User Management
- **Registration**: Users can create accounts with email and password
- **Login/Logout**: Secure authentication with JWT tokens stored in cookies
- **User Profiles**: Display user information, reputation, questions, and answers
- **Avatar System**: Integration with Gravatar for user avatars
- **Ban System**: Admins can ban users from posting content

### 2. Question & Answer System
- **Ask Questions**: Users can post questions with title, content, and tags
- **Answer Questions**: Users can provide answers to help others
- **Accept Answers**: Question authors can mark the best answer as "accepted"
- **Edit Questions**: Authors can edit their own questions
- **Vote System**: Upvote/downvote questions and answers
- **Question Status**: Track if questions are open, solved, or closed

### 3. Comments
- **Question Comments**: Add comments to questions for clarification
- **Answer Comments**: Comment on answers for follow-up discussion
- **Real-time Updates**: Comments appear immediately after posting

### 4. Tags System
- **Tag Creation**: Automatic tag creation when asking questions
- **Tag Pages**: Browse questions by specific tags
- **Tag Search**: Find tags by name
- **Popular Tags**: Display trending tags based on usage

### 5. Search & Discovery
- **Question Search**: Search questions by title and content
- **User Search**: Find users by username
- **Tag Search**: Search for specific tags
- **Sorting Options**: Sort by newest, popular, active, views, or unanswered
- **Pagination**: Navigate through large lists of content

### 6. Reputation System
- **Earn Points**: Get reputation for helpful contributions
- **Accept Answer**: +15 reputation when your answer is accepted
- **Upvotes**: Earn reputation from community votes
- **Leaderboard**: View top contributors by reputation

### 7. Admin Panel
- **Separate Login**: Dedicated admin login at `/admin/login`
- **User Management**: View all users with search and filters
- **Ban/Unban Users**: Prevent or allow users from posting
- **Statistics Dashboard**: View platform statistics
- **Cookie-based Auth**: Simple session management for admins

### 8. UI/UX Features
- **Responsive Design**: Works on desktop, tablet, and mobile
- **Loading States**: Skeleton loaders and spinners
- **Error Handling**: User-friendly error messages
- **Toast Notifications**: Success/error feedback
- **Breadcrumb Navigation**: Easy navigation through pages
- **Consistent Theme**: Gray-50 background across all pages

---

## Database Schema

### User Model
```typescript
{
  username: String (unique, required)
  email: String (unique, required)
  passwordHash: String (required)
  bio: String
  avatar: String (URL)
  reputation: Number (default: 0)
  createdAt: Date
  lastActiveAt: Date
  isBanned: Boolean
  bannedAt: Date
}
```

### Question Model
```typescript
{
  title: String (required)
  content: String (required)
  author: ObjectId (ref: User)
  tags: [ObjectId] (ref: Tag)
  answers: [ObjectId] (ref: Answer)
  votes: Number (default: 0)
  views: Number (default: 0)
  status: String (open/solved/closed)
  upvotedBy: [ObjectId] (ref: User)
  downvotedBy: [ObjectId] (ref: User)
  createdAt: Date
  updatedAt: Date
}
```

### Answer Model
```typescript
{
  content: String (required)
  author: ObjectId (ref: User)
  question: ObjectId (ref: Question)
  votes: Number (default: 0)
  isAccepted: Boolean (default: false)
  upvotedBy: [ObjectId] (ref: User)
  downvotedBy: [ObjectId] (ref: User)
  createdAt: Date
  updatedAt: Date
}
```

### Tag Model
```typescript
{
  name: String (unique, required)
  slug: String (unique, required)
  description: String
  icon: String (emoji)
  usageCount: Number (default: 0)
  createdAt: Date
}
```

### Comment Model
```typescript
{
  content: String (required)
  author: ObjectId (ref: User)
  parentType: String ('question' or 'answer')
  parentId: ObjectId
  votes: Number (default: 0)
  createdAt: Date
}
```

---

## API Routes

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/logout` - Logout user
- `GET /api/auth/me` - Get current user

### Questions
- `GET /api/questions` - Get all questions (with pagination & filters)
- `POST /api/questions` - Create new question
- `GET /api/questions/[id]` - Get question by ID
- `PUT /api/questions/[id]` - Update question
- `DELETE /api/questions/[id]` - Delete question
- `POST /api/questions/[id]/vote` - Vote on question
- `POST /api/questions/[id]/answers` - Post answer to question
- `GET /api/questions/[id]/comments` - Get question comments
- `POST /api/questions/[id]/comments` - Add comment to question

### Answers
- `POST /api/answers/[id]/vote` - Vote on answer
- `POST /api/answers/[id]/accept` - Accept answer
- `GET /api/answers/[id]/comments` - Get answer comments
- `POST /api/answers/[id]/comments` - Add comment to answer

### Users
- `GET /api/users` - Get all users (with pagination)
- `GET /api/users/[id]` - Get user profile

### Tags
- `GET /api/tags` - Get all tags
- `GET /api/tags/[slug]` - Get tag details and related questions

### Search
- `GET /api/search/questions` - Search questions
- `GET /api/search/users` - Search users
- `GET /api/search/tags` - Search tags

### Statistics
- `GET /api/stats` - Get platform statistics

### Admin
- `POST /api/admin/auth/login` - Admin login
- `POST /api/admin/auth/logout` - Admin logout
- `GET /api/admin/users` - Get users list (admin only)
- `POST /api/admin/users/[id]/ban` - Ban/unban user (admin only)

---

## Authentication System

### User Authentication
- **JWT Tokens**: Stored in HTTP-only cookies
- **Password Hashing**: Using bcrypt with salt rounds
- **Session Management**: 7-day token expiration
- **Protected Routes**: Middleware checks authentication
- **Context Provider**: React context for auth state

### Admin Authentication
- **Separate System**: Independent from user auth
- **Cookie-based**: Simple session management
- **Environment Variables**: Credentials stored in .env
- **Default Credentials**: admin / admin123
- **8-hour Sessions**: Automatic logout after 8 hours

---

## Admin Panel

### Features
- **Dashboard**: View statistics and user overview
- **User Management**: Search, filter, and manage users
- **Ban System**: Ban/unban users with timestamp tracking
- **Server-side Enforcement**: Banned users cannot post questions, answers, or comments
- **Filters**: View all users, only banned, or only active users
- **Search**: Find users by username or email
- **Pagination**: Navigate through user lists

### Access
- URL: `http://localhost:3000/admin/login`
- Default username: `admin`
- Default password: `admin123`
- Change credentials in `.env.local` file

---

## Setup Instructions

### Prerequisites
- Node.js 18+ installed
- MongoDB installed and running

### Installation Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/fixbuddy.git
   cd fixbuddy
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Create environment file**
   Create `.env.local` file in root directory:
   ```env
   MONGODB_URI=mongodb://localhost:27017/fixbuddy
   JWT_SECRET=your-secret-key-here-change-in-production
   ADMIN_USERNAME=admin
   ADMIN_PASSWORD=admin123
   ```

4. **Seed the database** (Optional but recommended)
   ```bash
   npx tsx scripts/seed.ts
   ```
   This creates:
   - 5 sample users
   - 10 tags
   - 8 questions
   - ~20 answers
   - 10 comments

5. **Run development server**
   ```bash
   npm run dev
   ```

6. **Open browser**
   Navigate to `http://localhost:3000`

### Test Credentials
After seeding, you can login with:
- **Email**: john@fixbuddy.com
- **Password**: password123

All seeded users have the same password: `password123`

---

## Key Components

### 1. Navbar (`components/Navbar.tsx`)
- Global navigation bar
- User authentication status
- Links to main sections
- Search functionality
- Login/Register buttons or user menu

### 2. QuestionCard (`components/QuestionCard.tsx`)
- Displays question summary
- Shows votes, answers, views
- Tags display
- Author information
- Status indicator (solved/open)

### 3. AnswerCard (`components/AnswerCard.tsx`)
- Shows answer content
- Vote buttons
- Accept answer button (for question author)
- Author details
- Timestamp
- Comment section

### 4. VoteButton (`components/VoteButton.tsx`)
- Upvote/downvote functionality
- Visual feedback for user's vote
- Optimistic updates
- API integration

### 5. CommentSection (`components/CommentSection.tsx`)
- Display comments
- Add new comments
- Nested comment structure
- Real-time updates

### 6. QuestionForm (`components/QuestionForm.tsx`)
- Create/edit questions
- Tag selection
- Content editor
- Validation

### 7. UserAvatar (`components/UserAvatar.tsx`)
- Display user avatars
- Gravatar integration
- Fallback to initials
- Size variants

### 8. AuthContext (`contexts/AuthContext.tsx`)
- Global authentication state
- Login/logout functions
- User data management
- Protected route handling

---

## How Everything Works Together

### Flow: Asking a Question

1. User clicks "Ask Question" in navbar
2. Redirected to `/ask` page
3. Fills out QuestionForm with title, content, and tags
4. On submit, POST request to `/api/questions`
5. API validates user authentication
6. Checks if user is banned
7. Creates question in database
8. Returns question data
9. User redirected to new question page

### Flow: Answering a Question

1. User views question at `/questions/[id]`
2. Scrolls to "Your Answer" section
3. Types answer in SimpleTextArea
4. Clicks "Post Your Answer"
5. POST request to `/api/questions/[id]/answers`
6. API validates authentication and ban status
7. Creates answer in database
8. Updates question's answer count
9. Answer appears on page
10. Answerer gets reputation if accepted

### Flow: Admin Banning a User

1. Admin logs in at `/admin/login`
2. Views dashboard with user list
3. Searches for specific user
4. Clicks "Ban" button next to user
5. POST request to `/api/admin/users/[id]/ban`
6. Updates user's `isBanned` status
7. User immediately cannot post content
8. All content APIs check ban status

### Flow: Voting

1. User clicks upvote/downvote button
2. VoteButton sends POST to `/api/questions/[id]/vote` or `/api/answers/[id]/vote`
3. API checks if user already voted
4. Updates vote count in database
5. Updates user's vote status
6. Returns new vote count
7. Component updates UI optimistically

---

## Important Notes

### Ban System
- Banned users **cannot** create questions, answers, or comments
- Ban check happens at API level (server-side)
- Cannot be bypassed from frontend
- Ban status checked on every content creation request

### Reputation System
- +15 points when your answer is accepted
- Points earned from upvotes (not fully implemented)
- Displayed on user profiles
- Used for leaderboard ranking

### Avatar System
- Automatic Gravatar integration based on email
- Falls back to user initials if no Gravatar
- Can use custom avatar URLs
- Seed script uses DiceBear avatars for demo

### Data Consistency
- Solved questions always have an accepted answer
- Question's answer array matches actual answers
- User reputation reflects accepted answers
- Tag usage counts are accurate

---

## Future Improvements

### Potential Features to Add
1. **Email Notifications**: Notify users of answers/comments
2. **Rich Text Editor**: Better formatting for questions/answers
3. **Image Upload**: Attach images to questions/answers
4. **Badge System**: Achievements for contributions
5. **Bookmarks**: Save favorite questions
6. **Follow Users**: Get updates from specific users
7. **Markdown Support**: Format content with markdown
8. **Code Syntax Highlighting**: For technical solutions
9. **Duplicate Detection**: Suggest similar questions
10. **Report System**: Flag inappropriate content

### Technical Improvements
1. **Real-time Updates**: WebSocket for live updates
2. **Caching**: Redis for improved performance
3. **Search Enhancement**: Elasticsearch for better search
4. **Image Optimization**: CDN for avatar storage
5. **Rate Limiting**: Prevent spam and abuse
6. **API Documentation**: Swagger/OpenAPI docs
7. **Testing**: Unit and integration tests
8. **Monitoring**: Error tracking and analytics
9. **SEO Optimization**: Meta tags and sitemap
10. **Progressive Web App**: Offline functionality

---

## Conclusion

FixBuddy is a fully functional Q&A platform built with modern web technologies. It demonstrates:
- Full-stack development with Next.js
- Database design with MongoDB
- Authentication and authorization
- RESTful API design
- React component architecture
- TypeScript for type safety
- Responsive UI with Tailwind CSS

The project is structured for scalability and maintainability, with clear separation of concerns between components, API routes, and database models.

---

**Last Updated**: October 21, 2025
**Version**: 1.0.0
**Author**: FixBuddy Team
