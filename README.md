# AI Code Reviewer 🤖

A powerful, feature-rich web application that leverages Google Gemini AI to provide instant, intelligent code reviews. Perfect for learning, improving code quality, and following best practices.

## ✨ Features

### Core Features

- **Instant AI Code Reviews**: Get comprehensive reviews powered by Google's Gemini 2.0 Flash
- **Multi-Language Support**: JavaScript, TypeScript, Python, Java, C++, C#, PHP, Ruby, Go, and Rust
- **Multiple Review Types**:
  - General Review: Overall code quality assessment
  - Performance Analysis: Optimization and complexity analysis
  - Security Audit: Vulnerability and security best practices
  - Best Practices: Code standards and design patterns
- **Syntax Highlighting**: Beautiful code editor with language-specific highlighting
- **Dark/Light Mode**: Theme toggle for comfortable viewing

### Smart Features

- **Usage Limits**: 5 reviews per day, 100 per month (free tier optimized)
- **Review History**: Keep track of all your reviews locally
- **Favorites**: Mark important reviews for quick access
- **Export Options**: Download reviews as text files
- **Copy Functionality**: Copy code or reviews to clipboard
- **Real-time Stats**: View your usage limits and remaining reviews

### User Experience

- **Responsive Design**: Works seamlessly on desktop, tablet, and mobile
- **Progressive Loading**: Loading states and smooth animations
- **Error Handling**: Clear error messages and retry options
- **Toast Notifications**: User feedback for actions and errors
- **Local Storage**: Reviews persist across browser sessions

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ or Docker
- Google Gemini API Key (get it free at [Google AI Studio](https://aistudio.google.com/app/apikey))

### Installation

#### Option 1: Local Development

1. **Clone and setup**

```bash
cd AI\ Code\ Reviewer
npm install
```

2. **Configure environment**

```bash
# Backend
cp backend/.env.example backend/.env
# Edit backend/.env and add your GEMINI_API_KEY

# Frontend
cp frontend/ai-code-reviewer/.env.example frontend/ai-code-reviewer/.env
```

3. **Install dependencies**

```bash
# Backend
cd backend
npm install
cd ..

# Frontend
cd frontend/ai-code-reviewer
npm install
cd ../..
```

4. **Start the application**

```bash
npm run dev
```

The application will be available at:

- Frontend: http://localhost:5173
- Backend API: http://localhost:3001

#### Option 2: Docker Deployment

1. **Configure environment**

```bash
cp backend/.env.example .env
# Edit .env and add your GEMINI_API_KEY
```

2. **Run with Docker Compose**

```bash
docker-compose up --build
```

The application will be available at:

- Frontend: http://localhost:5173
- Backend API: http://localhost:3001

## 📁 Project Structure

```
ai-code-reviewer/
├── backend/                 # Express.js server
│   ├── src/
│   │   ├── app.js          # Express app setup
│   │   ├── server.js       # Entry point
│   │   ├── controllers/
│   │   │   └── ai.controller.js
│   │   ├── routes/
│   │   │   └── ai.routes.js
│   │   ├── services/
│   │   │   └── ai.service.js
│   │   └── utils/
│   │       ├── logger.js
│   │       ├── tokenManager.js
│   │       ├── validation.js
│   │       └── errors.js
│   ├── Dockerfile
│   ├── package.json
│   └── .env.example
├── frontend/ai-code-reviewer/  # React + Vite
│   ├── src/
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   ├── index.css
│   │   ├── components/
│   │   │   ├── CodeEditor.jsx
│   │   │   ├── ReviewDisplay.jsx
│   │   │   ├── ReviewHistory.jsx
│   │   │   ├── UsageLimits.jsx
│   │   │   └── common/
│   │   │       ├── UI.jsx
│   │   │       └── LanguageSelector.jsx
│   │   ├── services/
│   │   │   └── api.js
│   │   └── store/
│   │       └── appStore.js
│   ├── Dockerfile
│   ├── nginx.conf
│   ├── tailwind.config.js
│   ├── postcss.config.js
│   ├── package.json
│   └── .env.example
├── docker-compose.yml
└── README.md
```

## 🔧 Technology Stack

### Backend

- **Node.js & Express.js**: Server framework
- **Google Gemini AI**: AI reviews
- **Winston**: Logging
- **Express Rate Limit**: DDoS protection
- **Helmet.js**: Security headers
- **Joi**: Input validation

### Frontend

- **React 19**: UI library
- **Vite**: Build tool
- **Zustand**: State management
- **Tailwind CSS**: Styling
- **Axios**: HTTP client
- **Prism.js**: Syntax highlighting
- **React Hot Toast**: Notifications
- **Lucide React**: Icons

## 📊 API Endpoints

### POST /ai/get-review

Submit code for review

**Request:**

```json
{
  "userCode": "function example() { ... }",
  "language": "javascript",
  "reviewType": "general"
}
```

**Response:**

```json
{
  "success": true,
  "response": "Review text...",
  "metadata": {
    "language": "javascript",
    "reviewType": "general",
    "timestamp": "2025-01-01T12:00:00Z"
  },
  "limits": {
    "daily": { "used": 1, "limit": 5, "remaining": 4 },
    "monthly": { "used": 1, "limit": 100, "remaining": 99 }
  }
}
```

### GET /ai/stats

Get current usage statistics

**Response:**

```json
{
  "success": true,
  "stats": {
    "daily": { "used": 1, "limit": 5, "remaining": 4 },
    "monthly": { "used": 1, "limit": 100, "remaining": 99 }
  }
}
```

### GET /health

Health check endpoint

## ⚙️ Configuration

### Environment Variables

**Backend (.env)**

```
GEMINI_API_KEY=your_api_key_here
PORT=3001
NODE_ENV=development
FRONTEND_URL=http://localhost:5173
LOG_LEVEL=info
```

**Frontend (.env)**

```
VITE_API_URL=http://localhost:3001
```

## 🎯 Usage Limits

The application implements smart rate limiting to keep within Google's free tier:

- **Daily Limit**: 5 reviews per day per IP
- **Monthly Limit**: 100 reviews per month per IP
- **Code Size**: Maximum 10,000 characters per review
- **Rate Limiting**: 100 requests per 15 minutes per IP

These limits can be adjusted in `backend/src/utils/tokenManager.js`

## 📈 Performance Optimizations

- **Code Splitting**: Lazy loading of components
- **Compression**: Gzip compression for HTTP
- **Caching**: Browser caching for static assets
- **Syntax Highlighting**: Efficient code highlighting with Prism.js
- **State Management**: Zustand for lightweight state
- **Responsive Images**: Optimized assets for different screen sizes

## 🔒 Security Features

- **Helmet.js**: HTTP security headers
- **CORS**: Cross-origin request handling
- **Input Validation**: Joi schema validation
- **Rate Limiting**: Prevent DDoS attacks
- **Error Handling**: Safe error messages
- **Async Error Handler**: Graceful error handling

## 📝 Logging

Application logs are written to:

- `backend/error.log`: Error logs
- `backend/combined.log`: All logs

Adjust log level in environment variable `LOG_LEVEL`

## 🧪 Testing

Run tests with:

```bash
# Backend (coming soon)
npm test

# Frontend (coming soon)
npm run test:ui
```

## 📦 Deployment

### Docker Deployment

Build and push images:

```bash
docker build -t ai-code-reviewer-backend ./backend
docker build -t ai-code-reviewer-frontend ./frontend/ai-code-reviewer
```

### Heroku Deployment

```bash
heroku login
heroku create ai-code-reviewer-backend
git push heroku main
```

### AWS ECS Deployment

```bash
# Build and push to ECR
aws ecr create-repository --repository-name ai-code-reviewer
docker tag ai-code-reviewer-backend:latest <account-id>.dkr.ecr.us-east-1.amazonaws.com/ai-code-reviewer:latest
docker push <account-id>.dkr.ecr.us-east-1.amazonaws.com/ai-code-reviewer:latest
```

## 🛣️ Future Features

- [ ] User authentication and profiles
- [ ] Database integration for persistent storage
- [ ] Code comparison tools
- [ ] Integration with GitHub/GitLab
- [ ] Batch file processing
- [ ] Custom review templates
- [ ] Team collaboration features
- [ ] Advanced analytics and progress tracking
- [ ] API access for developers
- [ ] Mobile app

## 🤝 Contributing

We welcome contributions! Please feel free to submit issues and pull requests.

## 📄 License

MIT License - feel free to use this project for personal or commercial purposes.

## 💝 Support

If you find this project helpful, please consider:

- Starring the repository
- Sharing it with your network
- Providing feedback and suggestions

## 🙋 FAQ

**Q: Do I need to create an account?**  
A: No! The app works anonymously without any account creation. Usage limits are based on your IP address.

**Q: How many reviews can I get?**  
A: 5 reviews per day and 100 per month on the free tier, to stay within Google's Gemini API free tier limits.

**Q: Is my code stored?**  
A: No! Your code is processed immediately and not stored on our servers. Reviews are stored locally in your browser.

**Q: Can I use this with other AI models?**  
A: Currently, it uses Google Gemini. You can modify the backend to use other APIs.

**Q: What languages are supported?**  
A: JavaScript, TypeScript, Python, Java, C++, C#, PHP, Ruby, Go, and Rust.

## 📞 Contact

For questions or suggestions, please open an issue on GitHub.

---

**Made with ❤️ using React, Express, and Google Gemini AI**
