# 🚀 A11yAll Deployment Guide

## 📋 Prerequisites

1. **GitHub Account** - Your code must be in a GitHub repository
2. **Vercel Account** - Sign up at [vercel.com](https://vercel.com)
3. **Groq API Key** - Get your free API key from [console.groq.com](https://console.groq.com)

---

## 🎯 Quick Deploy to Vercel (Recommended)

### Step 1: Push Code to GitHub
```bash
# If not already a git repository
git init
git add .
git commit -m "Initial commit - A11yAll ready for deployment"

# Create GitHub repository and push
git remote add origin https://github.com/YOUR_USERNAME/a11yall.git
git branch -M main
git push -u origin main
```

### Step 2: Deploy to Vercel
1. Go to [vercel.com](https://vercel.com) and sign in
2. Click **"New Project"**
3. Import your GitHub repository
4. Vercel will auto-detect the configuration from `vercel.json`
5. Click **"Deploy"**

### Step 3: Add Environment Variables
In Vercel dashboard:
1. Go to your project **Settings** → **Environment Variables**
2. Add: `GROQ_API_KEY` with your Groq API key value
3. **Redeploy** the project

---

## 🔧 Alternative: Manual Configuration

If auto-detection doesn't work, use these settings in Vercel:

### Build Settings:
- **Framework Preset:** Other
- **Root Directory:** `./`
- **Build Command:** `cd client && npm install && npm run build`
- **Output Directory:** `client/dist`
- **Install Command:** `npm install`

### Environment Variables:
```
GROQ_API_KEY=your_groq_api_key_here
```

---

## 🌐 Netlify Alternative

### Step 1: Create Netlify Configuration
Create `netlify.toml`:
```toml
[build]
  base = "client"
  command = "npm run build"
  publish = "dist"

[functions]
  directory = "server"

[[redirects]]
  from = "/api/*"
  to = "/.netlify/functions/server/:splat"
  status = 200

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

### Step 2: Convert Server for Netlify Functions
Create `server/netlify.js`:
```javascript
const serverless = require('serverless-http');
const app = require('./server.js');

module.exports.handler = serverless(app);
```

### Step 3: Deploy to Netlify
1. Go to [netlify.com](https://netlify.com)
2. Connect your GitHub repository
3. Set build settings:
   - **Base directory:** `client`
   - **Build command:** `npm run build`
   - **Publish directory:** `client/dist`
4. Add environment variable: `GROQ_API_KEY`

---

## ⚠️ Important Notes

### 🔒 **Serverless Limitations**
- **URL Scanning:** In production, Cypress tests won't run (serverless environment)
- **Alternative:** App provides manual testing guidance and tool recommendations
- **Local Development:** Full Cypress functionality works when running locally

### 🔑 **Security**
- Never commit API keys to GitHub
- Use environment variables for all sensitive data
- Groq API key is required for AI functionality

### 🧪 **Testing Deployment**
After deployment, test these features:
1. ✅ General accessibility questions
2. ✅ "Who built you?" → Should mention sgp
3. ✅ URL scanning → Should provide guidance (not live scan)
4. ✅ Responsive design
5. ✅ Dark theme accessibility

---

## 🎯 Your Deployed URLs

After successful deployment:
- **Live App:** `https://your-project-name.vercel.app`
- **API Endpoints:** 
  - `https://your-project-name.vercel.app/api/chat-general`
  - `https://your-project-name.vercel.app/api/scan-url`

---

## 🐛 Troubleshooting

### Build Fails?
```bash
# Test locally first
cd client
npm install
npm run build

cd ../server
npm install
npm start
```

### API Not Working?
1. Check environment variables in Vercel/Netlify dashboard
2. Verify Groq API key is valid
3. Check function logs in deployment dashboard

### Styling Issues?
- Clear browser cache
- Check if CSS files are loading in Network tab
- Verify Vite build output

---

## 🚀 Success!

Your A11yAll accessibility consultant is now live! 🎉

**Features Available:**
- ✅ AI-powered accessibility guidance
- ✅ Professional audit recommendations  
- ✅ Manual testing tool suggestions
- ✅ WCAG compliance advice
- ✅ Beautiful accessible dark theme
- ✅ Creator attribution to sgp

**Next Steps:**
- Share your deployment URL
- Test all functionality
- Monitor usage in Vercel/Netlify analytics
- Consider adding custom domain

---

*Created by sgp - Making accessibility accessible to everyone! 🌟* 