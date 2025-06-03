---
layout: default
title: DataLoud - AI-Powered Document Chatbot
permalink: /
---

<style>
/* Hero Section Styles */
.hero-section {
    padding: 6rem 2rem;
    text-align: center;
    background: radial-gradient(circle at 50% 0%, rgba(99, 102, 241, 0.15) 0%, rgba(99, 102, 241, 0.05) 30%, rgba(0, 0, 0, 0) 70%);
    min-height: 80vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
}

.hero-title {
    font-size: clamp(2.5rem, 8vw, 4rem);
    font-weight: 700;
    margin-bottom: 1.5rem;
    background: linear-gradient(135deg, #ffffff 0%, #a1a1aa 100%);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    line-height: 1.1;
}

.hero-description {
    font-size: 1.2rem;
    color: #9ca3af;
    max-width: 600px;
    margin: 0 auto 3rem;
    line-height: 1.6;
}

.cta-buttons {
    display: flex;
    gap: 1rem;
    justify-content: center;
    flex-wrap: wrap;
}

.btn {
    padding: 0.75rem 2rem;
    border-radius: 0.5rem;
    text-decoration: none;
    font-weight: 500;
    transition: all 0.3s ease;
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
}

.btn-primary {
    background: white;
    color: black;
}

.btn-primary:hover {
    background: #f3f4f6;
}

.btn-secondary {
    background: rgba(255, 255, 255, 0.1);
    color: white;
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.btn-secondary:hover {
    background: rgba(255, 255, 255, 0.2);
}

/* Features Section */
.features-section {
    padding: 6rem 2rem;
    background: rgba(255, 255, 255, 0.02);
}

.features-container {
    max-width: 1200px;
    margin: 0 auto;
}

.features-title {
    font-size: 3rem;
    font-weight: 700;
    text-align: center;
    margin-bottom: 4rem;
    background: linear-gradient(135deg, #ffffff 0%, #a1a1aa 100%);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}

.features-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 2rem;
}

.feature-card {
    padding: 2rem;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 1rem;
    text-align: center;
    transition: all 0.3s ease;
}

.feature-card:hover {
    background: rgba(255, 255, 255, 0.1);
    transform: translateY(-4px);
}

.feature-icon {
    font-size: 3rem;
    margin-bottom: 1rem;
}

.feature-card h3 {
    font-size: 1.25rem;
    margin-bottom: 0.5rem;
    color: white;
}

.feature-card p {
    color: #9ca3af;
    font-size: 0.875rem;
}

.nav-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
    margin-top: 3rem;
}

.nav-card {
    padding: 2rem;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 1rem;
    transition: all 0.3s ease;
}

.nav-card:hover {
    background: rgba(255, 255, 255, 0.1);
    transform: translateY(-4px);
}

.nav-card h3 {
    margin-bottom: 1rem;
    color: white;
}

.nav-card h3 a {
    color: white;
    text-decoration: none;
}

.nav-card h3 a:hover {
    color: #60a5fa;
}

.nav-card p {
    color: #9ca3af;
    font-size: 0.9rem;
}

@media (max-width: 768px) {
    .hero-section {
        padding: 4rem 1rem;
    }
    
    .cta-buttons {
        flex-direction: column;
        align-items: center;
    }
    
    .features-title {
        font-size: 2rem;
    }
}
</style>

<!-- Hero Section -->
<section class="hero-section" id="hero">
    <h1 class="hero-title">
        Transform Documents Into<br>Intelligent Conversations
    </h1>
    
    <p class="hero-description">
        Upload any document and chat with it using advanced AI. Get instant answers, summaries, and insights from your PDFs, Word docs, and more through natural language conversations.
    </p>
    
    <div class="cta-buttons">
        <a href="#demo" class="btn btn-secondary">
            ▶️ Live Demo
        </a>
        <a href="#get-started" class="btn btn-primary">
            Try Now
        </a>
    </div>
</section>

<!-- Quick Navigation -->
<section class="features-section">
    <div class="features-container">
        <h2 class="features-title">🚀 Quick Navigation</h2>
        
        <div class="nav-grid">
            <div class="nav-card">
                <h3>📖 <a href="./README">Complete Overview</a></h3>
                <p>Full project documentation with features and architecture</p>
            </div>
            
            <div class="nav-card">
                <h3>👤 <a href="./USER_GUIDE">User Guide</a></h3>
                <p>Get started in 3 simple steps and learn best practices</p>
            </div>
            
            <div class="nav-card">
                <h3>📡 <a href="./API">API Reference</a></h3>
                <p>Complete API documentation and integration examples</p>
            </div>
            
            <div class="nav-card">
                <h3>🏗️ <a href="./ARCHITECTURE">Architecture</a></h3>
                <p>Technical specifications and system design</p>
            </div>
        </div>
    </div>
</section>

<!-- Features Section -->
<section class="features-section" id="features">
    <div class="features-container">
        <h2 class="features-title">Powerful Features</h2>
        
        <div class="features-grid">
            <div class="feature-card">
                <div class="feature-icon">📄</div>
                <h3>Multi-Format Support</h3>
                <p>PDF, Word, PowerPoint, Excel, and more</p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">🧠</div>
                <h3>Advanced AI</h3>
                <p>RAG-based architecture for accurate responses</p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">🔒</div>
                <h3>Secure & Private</h3>
                <p>Your documents stay private and secure</p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">⚡</div>
                <h3>Real-time Chat</h3>
                <p>Instant responses and contextual understanding</p>
            </div>
        </div>
    </div>
</section>

<!-- Get Started Section -->
<section class="features-section" id="get-started">
    <div class="features-container">
        <h2 class="features-title">Ready to Get Started?</h2>
        
        <div style="text-align: center; max-width: 600px; margin: 0 auto;">
            <p style="color: #9ca3af; font-size: 1.2rem; margin-bottom: 3rem;">
                Join thousands of users who are already transforming how they interact with documents.
            </p>
            
            <div class="cta-buttons">
                <a href="./USER_GUIDE" class="btn btn-primary">
                    📖 User Guide
                </a>
                <a href="./API" class="btn btn-secondary">
                    🔧 API Docs
                </a>
            </div>
        </div>
    </div>
</section>

<script>
// Add smooth scrolling
document.addEventListener('DOMContentLoaded', function() {
    document.querySelectorAll('a[href^="#"]').forEach(anchor => {
        anchor.addEventListener('click', function (e) {
            e.preventDefault();
            const target = document.querySelector(this.getAttribute('href'));
            if (target) {
                target.scrollIntoView({
                    behavior: 'smooth',
                    block: 'start'
                });
            }
        });
    });
    
    // Add parallax effect
    window.addEventListener('scroll', () => {
        const scrolled = window.pageYOffset;
        const hero = document.querySelector('#hero');
        if (hero) {
            hero.style.transform = `translateY(${scrolled * 0.3}px)`;
        }
    });
});
</script>
    <p>Complete API documentation for developers</p>
  </div>
  
  <div class="nav-card">
    <h3>🏗️ <a href="./ARCHITECTURE">Architecture</a></h3>
    <p>Technical system design and components</p>
  </div>
  
  <div class="nav-card">
    <h3>🚀 <a href="./DEPLOYMENT">Deployment</a></h3>
    <p>Production deployment guide and setup</p>
  </div>
  
  <div class="nav-card">
    <h3>🤝 <a href="./CONTRIBUTING">Contributing</a></h3>
    <p>Guidelines for developers and contributors</p>
  </div>
</div>

## ✨ Key Features

### 🔍 **Smart Document Processing**
- **Multi-format Support**: PDF, CSV, JSON documents
- **Intelligent Chunking**: Advanced text segmentation
- **Vector Embeddings**: Semantic search capabilities
- **Real-time Processing**: Fast document analysis

### 💬 **Advanced AI Chat**
- **Natural Language**: Ask questions in plain English
- **Context Awareness**: Maintains conversation flow
- **Source Citations**: References document sections
- **Multi-turn Dialogues**: Complex conversations

### 🎨 **Modern Interface**
- **Responsive Design**: Works on all devices
- **Real-time Updates**: Live chat experience
- **Dark/Light Mode**: Customizable themes
- **Drag & Drop**: Easy file uploads

## 🏗️ System Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │    Backend      │    │   Database      │
│   (Next.js)     │◄──►│   (Flask)       │◄──►│  (Supabase)     │
│                 │    │                 │    │                 │
│ • React UI      │    │ • RAG Pipeline  │    │ • PostgreSQL    │
│ • TypeScript    │    │ • Vector Store  │    │ • Vector Ext    │
│ • Tailwind CSS  │    │ • AI Integration│    │ • RLS Policies  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 📊 Performance Highlights

- **⚡ Fast Processing**: < 5 seconds for document upload
- **🔍 Quick Search**: < 500ms vector similarity search
- **👥 Scalable**: 100+ concurrent users supported
- **🛡️ Secure**: Row-level security and data isolation

## 🎯 Use Cases

- **📚 Research**: Academic paper analysis
- **💼 Business**: Corporate document review
- **🎓 Education**: Study material interaction
- **⚖️ Legal**: Contract and document analysis
- **✍️ Content**: Reference material organization

## 🔗 Repository Links

- **📂 [View on GitHub](https://github.com/PaoloAstrino/DataLoud_public)**
- **📋 [Complete Documentation](./DOCUMENTATION_INDEX)**
- **🌟 [Star this Project](https://github.com/PaoloAstrino/DataLoud_public)**

---

<div class="footer-section">
  <p><strong>🎉 Ready to explore?</strong> Start with the <a href="./USER_GUIDE">User Guide</a> or dive into the <a href="./ARCHITECTURE">technical architecture</a>!</p>
  
  <p><em>This project showcases production-ready AI/ML development with modern web technologies.</em></p>
</div>

<style>
.navigation-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  margin: 30px 0;
}

.nav-card {
  border: 1px solid #e1e4e8;
  border-radius: 8px;
  padding: 20px;
  background: #f6f8fa;
  transition: transform 0.2s, box-shadow 0.2s;
}

.nav-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.nav-card h3 {
  margin-top: 0;
  margin-bottom: 10px;
}

.nav-card h3 a {
  text-decoration: none;
  color: #0366d6;
}

.nav-card h3 a:hover {
  text-decoration: underline;
}

.nav-card p {
  margin-bottom: 0;
  color: #586069;
}

.footer-section {
  text-align: center;
  padding: 30px 0;
  border-top: 1px solid #e1e4e8;
  margin-top: 50px;
}

@media (prefers-color-scheme: dark) {
  .nav-card {
    background: #161b22;
    border-color: #30363d;
  }
  
  .nav-card p {
    color: #8b949e;
  }
  
  .footer-section {
    border-top-color: #30363d;
  }
}
</style>
