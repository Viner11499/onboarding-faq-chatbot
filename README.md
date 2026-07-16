# Onboarding FAQ Chatbot

An AI-powered chatbot that helps new employees find answers about company onboarding, HR policies, IT setup, benefits, leave, payroll, security, equipment, and general company information.

## Features

✨ **Employee Chat Interface**
- ChatGPT-like chat interface
- Conversation history
- Typing indicators
- Suggested questions
- Mobile responsive
- Dark mode support

🤖 **AI-Powered Responses**
- Uses OpenAI API with Retrieval-Augmented Generation (RAG)
- Semantic search with embeddings
- Cites sources from knowledge base
- Only answers using company knowledge
- Never invents information

📚 **Knowledge Base Management**
- Admin dashboard to manage FAQs
- Add, edit, delete FAQs
- Upload PDF documents
- Upload DOCX files
- Automatic text extraction
- Support for multiple categories

🔐 **Security**
- JWT authentication
- Password hashing with bcrypt
- Input validation
- SQL injection prevention
- XSS protection
- CORS enabled
- Helmet security headers

📊 **Analytics**
- Track total FAQs
- Monitor uploaded documents
- View chat statistics
- Identify most asked questions
- Search analytics

## Tech Stack

- **Frontend**: React + TypeScript + Vite
- **Backend**: Node.js + Express + TypeScript
- **Database**: SQLite with Prisma ORM
- **AI**: OpenAI API
- **Vector Search**: Local embeddings
- **Styling**: Tailwind CSS + Framer Motion
- **Authentication**: JWT + bcrypt
- **Containerization**: Docker

## Project Structure

```
onboarding-faq-chatbot/
├── backend/                 # Express API
│   ├── src/
│   │   ├── server.ts
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── services/
│   │   ├── middleware/
│   │   ├── utils/
│   │   ├── types/
│   │   └── db/
│   ├── prisma/
│   ├── tests/
│   └── package.json
├── frontend/                # React app
│   ├── src/
│   │   ├── pages/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── types/
│   │   ├── utils/
│   │   └── App.tsx
│   └── package.json
��── docker-compose.yml
├── Dockerfile
└── README.md
```

## Quick Start

### Prerequisites

- Node.js 18+
- npm 9+
- OpenAI API key
- Docker (optional)

### Installation

1. Clone the repository
```bash
git clone <repository-url>
cd onboarding-faq-chatbot
```

2. Install dependencies
```bash
npm install
```

3. Set up environment variables
```bash
# Backend
cp backend/.env.example backend/.env

# Frontend
cp frontend/.env.example frontend/.env
```

4. Update `.env` files with your configuration
```bash
# backend/.env
OPENAI_API_KEY=your_key_here
DATABASE_URL=file:./dev.db
JWT_SECRET=your_secret_here
ADMIN_EMAIL=admin@company.com
ADMIN_PASSWORD=secure_password

# frontend/.env
VITE_API_URL=http://localhost:5000
```

5. Initialize database
```bash
cd backend
npx prisma migrate dev
npm run seed
```

6. Start development servers
```bash
npm run backend    # Terminal 1 - starts on port 5000
npm run frontend   # Terminal 2 - starts on port 5173
```

7. Open http://localhost:5173 in your browser

## Usage

### For Employees

1. **Sign In** - Use your company credentials (initially use admin account)
2. **Chat** - Ask questions about onboarding, policies, benefits, etc.
3. **Get Answers** - AI chatbot responds with information from knowledge base
4. **Follow Up** - Ask follow-up questions maintaining context

### For Admins

1. **Sign In** - Use admin credentials
2. **Manage FAQs** - Add, edit, or delete FAQ entries
3. **Upload Documents** - Upload PDF, DOCX, or policy files
4. **View Analytics** - Monitor chatbot usage and popular questions
5. **Manage Categories** - Organize knowledge by HR, IT, Payroll, Benefits, etc.

## API Endpoints

### Authentication
- `POST /api/auth/login` - Login with email and password
- `POST /api/auth/logout` - Logout
- `GET /api/auth/me` - Get current user

### Chat
- `POST /api/chat` - Send message and get response
- `GET /api/chat/history` - Get conversation history
- `DELETE /api/chat/history/:id` - Delete conversation

### FAQ Management (Admin)
- `GET /api/faqs` - List all FAQs
- `POST /api/faqs` - Create new FAQ
- `PUT /api/faqs/:id` - Update FAQ
- `DELETE /api/faqs/:id` - Delete FAQ
- `GET /api/faqs/category/:category` - Get FAQs by category

### Document Upload (Admin)
- `POST /api/documents/upload` - Upload document
- `GET /api/documents` - List uploaded documents
- `DELETE /api/documents/:id` - Delete document

### Analytics
- `GET /api/analytics/overview` - Dashboard overview
- `GET /api/analytics/questions` - Most asked questions
- `GET /api/analytics/search` - Search analytics

## Environment Variables

### Backend

```env
# Server
PORT=5000
NODE_ENV=development

# Database
DATABASE_URL=file:./dev.db

# Authentication
JWT_SECRET=your-super-secret-key-change-in-production
JWT_EXPIRY=7d

# OpenAI
OPENAI_API_KEY=sk-...
OPENAI_MODEL=gpt-4

# Admin
ADMIN_EMAIL=admin@company.com
ADMIN_PASSWORD=SecurePassword123!

# CORS
CORS_ORIGIN=http://localhost:5173

# File Upload
MAX_FILE_SIZE=10485760
ALLOWED_EXTENSIONS=pdf,docx,doc,txt
```

### Frontend

```env
VITE_API_URL=http://localhost:5000
VITE_APP_NAME=Onboarding FAQ Chatbot
```

## Database Schema

### Users
```sql
- id (UUID)
- email (unique)
- name
- password (hashed)
- role (admin, employee)
- createdAt
- updatedAt
```

### FAQs
```sql
- id (UUID)
- question
- answer
- category (HR, IT, Payroll, Benefits, Leave, etc.)
- order
- createdAt
- updatedAt
```

### Documents
```sql
- id (UUID)
- filename
- filePath
- fileType (pdf, docx, txt)
- content (extracted text)
- uploadedAt
```

### ChatHistory
```sql
- id (UUID)
- userId
- question
- answer
- sources (referenced documents/FAQs)
- timestamp
```

### ChatEmbeddings
```sql
- id (UUID)
- content
- embedding (vector)
- documentId
- faqId
- createdAt
```

## Security Features

- ✅ Password hashing with bcrypt
- ✅ JWT token authentication
- ✅ Helmet for HTTP headers
- ✅ CORS protection
- ✅ Input validation with Zod
- ✅ SQL injection prevention with Prisma
- ✅ XSS protection
- ✅ Rate limiting on API endpoints
- ✅ Secure password reset flow
- ✅ Session management

## Development

### Running Tests

```bash
npm run test
```

### Linting

```bash
npm run lint
```

### Format Code

```bash
npm run format
```

## Deployment

### Docker Deployment

```bash
docker-compose up -d
```

### Environment Setup for Production

Update `.env` files:
- Set `NODE_ENV=production`
- Update `DATABASE_URL` to production database
- Change `JWT_SECRET` to secure random value
- Update `CORS_ORIGIN` to production domain
- Add production OpenAI API key

## File Categories Supported

- HR & Onboarding
- IT Support
- Payroll & Compensation
- Benefits
- Leave & Time Off
- Attendance
- Remote Work
- Equipment & Resources
- Security & Compliance
- Company Culture
- Holidays
- Learning & Development
- Performance Reviews
- Office Locations
- Emergency Contacts

## FAQ Structure

The chatbot uses a structured FAQ system with:

- **Question** - Natural language question
- **Answer** - Comprehensive answer
- **Category** - Topic classification
- **Keywords** - For semantic search
- **Related FAQs** - Link to related questions
- **Last Updated** - Modification timestamp

## Troubleshooting

### OpenAI API Errors
- Verify API key in `.env`
- Check API quota and usage
- Ensure model name is correct

### Database Issues
- Run `npx prisma migrate dev` to apply migrations
- Check `DATABASE_URL` configuration
- Clear SQLite database if needed: `rm backend/dev.db`

### CORS Errors
- Verify `CORS_ORIGIN` matches frontend URL
- Check backend server is running

### Port Already in Use
- Backend: Change `PORT` in `.env`
- Frontend: Use `npm run dev -- --port 3000` in frontend directory

## Contributing

1. Create feature branch
2. Make changes
3. Run tests and linting
4. Submit pull request

## License

Proprietary - Internal Use Only

## Support

For issues or questions, contact the Development team or HR department.
