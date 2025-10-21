# FixBuddy 🔧

A community-driven Q&A platform for home appliance repairs and troubleshooting. Built with Next.js, TypeScript, and MongoDB.

![Next.js](https://img.shields.io/badge/Next.js-15.5.6-black)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue)
![MongoDB](https://img.shields.io/badge/MongoDB-Latest-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 🎯 Features

- **Question & Answer System** - Ask questions and get expert answers
- **Voting System** - Upvote/downvote helpful content
- **Accepted Answers** - Mark the best solution to your problem
- **Tags & Categories** - Organize questions by appliance type
- **User Profiles** - Track reputation and contributions
- **Comments** - Discuss questions and answers
- **Search & Filter** - Find solutions quickly
- **Admin Panel** - Manage users and moderate content
- **Ban System** - Prevent spam and abuse
- **Responsive Design** - Works on all devices

## 🚀 Quick Start

### Prerequisites

- Node.js 18 or higher
- MongoDB (local or Atlas)

### Installation

1. Clone the repository
```bash
git clone https://github.com/yourusername/fixbuddy.git
cd fixbuddy
```

2. Install dependencies
```bash
npm install
```

3. Create `.env.local` file
```env
MONGODB_URI=mongodb://localhost:27017/fixbuddy
JWT_SECRET=your-secret-key-here
ADMIN_USERNAME=admin
ADMIN_PASSWORD=admin123
```

4. Seed the database (optional)
```bash
npx tsx scripts/seed.ts
```

5. Run the development server
```bash
npm run dev
```

6. Open [http://localhost:3000](http://localhost:3000)

## 📚 Documentation

For detailed documentation about the project architecture, features, and implementation, see [PROJECT.md](./PROJECT.md).

## 🔐 Test Credentials

After seeding the database:
- **User Login**: john@fixbuddy.com / password123
- **Admin Panel**: admin / admin123 (at `/admin/login`)

## 🛠️ Tech Stack

- **Framework**: Next.js 15.5.6 with App Router
- **Language**: TypeScript
- **Database**: MongoDB with Mongoose
- **Styling**: Tailwind CSS
- **Authentication**: JWT with HTTP-only cookies
- **Development**: Turbopack for fast builds

## 📁 Project Structure

```
fixbuddy/
├── app/                    # Next.js App Router
│   ├── api/               # API endpoints
│   ├── admin/             # Admin panel
│   ├── questions/         # Question pages
│   └── ...
├── components/            # React components
├── lib/                   # Utilities and models
├── scripts/               # Database seeding
└── types/                 # TypeScript definitions
```

## 🎨 Key Features

### For Users
- Ask and answer questions
- Vote on helpful content
- Earn reputation points
- Comment and discuss
- Search by tags or keywords
- View user profiles

### For Admins
- Dedicated admin panel
- User management
- Ban/unban functionality
- Platform statistics
- Content moderation

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is licensed under the MIT License.

## 🙋‍♂️ Support

For questions or issues, please open an issue on GitHub.

## 🔗 Links

- [Detailed Documentation](./PROJECT.md)
- [MongoDB Setup Guide](https://www.mongodb.com/docs/manual/installation/)
- [Next.js Documentation](https://nextjs.org/docs)

---

**Built with ❤️ using Next.js and TypeScript**
