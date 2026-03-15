<template>
  <div class="landing-page">
    <!-- Navigation -->
    <nav class="navbar">
      <div class="nav-container">
        <div class="nav-brand" @click="scrollToTop">
          <span class="brand-icon">🐟</span>
          <span class="brand-text">Fish Predictions</span>
        </div>
        
        <div class="nav-links">
          <a href="#features" class="nav-link">Features</a>
          <a href="#how-it-works" class="nav-link">How It Works</a>
          <a href="#pricing" class="nav-link">Pricing</a>
          <a href="#faq" class="nav-link">FAQ</a>
        </div>
        
        <div class="nav-actions">
          <router-link to="/login" class="btn-login">Log In</router-link>
          <router-link to="/signup" class="btn-signup">Get Started Free</router-link>
        </div>
        
        <button class="mobile-menu-btn" @click="toggleMobileMenu">
          <span></span>
          <span></span>
          <span></span>
        </button>
      </div>
      
      <!-- Mobile Menu -->
      <div class="mobile-menu" :class="{ 'active': mobileMenuOpen }">
        <a href="#features" class="mobile-link" @click="closeMobileMenu">Features</a>
        <a href="#how-it-works" class="mobile-link" @click="closeMobileMenu">How It Works</a>
        <a href="#pricing" class="mobile-link" @click="closeMobileMenu">Pricing</a>
        <a href="#faq" class="mobile-link" @click="closeMobileMenu">FAQ</a>
        <div class="mobile-actions">
          <router-link to="/login" class="btn-login">Log In</router-link>
          <router-link to="/signup" class="btn-signup">Get Started Free</router-link>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-bg">
        <div class="hero-gradient"></div>
        <div class="hero-grid"></div>
      </div>
      
      <div class="hero-content">
        <div class="hero-badge">
          <span class="badge-icon">✨</span>
          <span>Powered by Advanced AI Agents</span>
        </div>
        
        <h1 class="hero-title">
          Predict the Future with<br>
          <span class="gradient-text">Swarm Intelligence</span>
        </h1>
        
        <p class="hero-subtitle">
          Upload any document and watch millions of AI agents simulate real-world scenarios. 
          Make data-driven decisions before they happen.
        </p>
        
        <div class="hero-cta">
          <router-link to="/signup" class="btn-primary">
            Start Free Trial
            <span class="btn-arrow">→</span>
          </router-link>
          <a href="#demo" class="btn-secondary">
            <span class="play-icon">▶</span>
            Watch Demo
          </a>
        </div>
        
        <div class="hero-stats">
          <div class="stat-item">
            <span class="stat-value">1M+</span>
            <span class="stat-label">Agents per Simulation</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat-item">
            <span class="stat-value">~$5</span>
            <span class="stat-label">Average Cost</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat-item">
            <span class="stat-value">10min</span>
            <span class="stat-label">Time to Insights</span>
          </div>
        </div>
      </div>
      
      <div class="hero-visual">
        <div class="visual-container">
          <div class="visual-card main-card">
            <div class="card-header">
              <span class="card-dot green"></span>
              <span class="card-dot yellow"></span>
              <span class="card-dot red"></span>
            </div>
            <div class="card-content">
              <div class="simulation-preview">
                <div class="agent-cluster">
                  <div class="agent" v-for="i in 12" :key="i" :style="getAgentStyle(i)"></div>
                </div>
                <div class="connection-lines">
                  <svg viewBox="0 0 200 200">
                    <line x1="50" y1="50" x2="150" y2="50" stroke="#FF4500" stroke-width="1" opacity="0.3"/>
                    <line x1="50" y1="100" x2="150" y2="150" stroke="#FF4500" stroke-width="1" opacity="0.3"/>
                    <line x1="100" y1="50" x2="100" y2="150" stroke="#FF4500" stroke-width="1" opacity="0.3"/>
                  </svg>
                </div>
              </div>
            </div>
          </div>
          
          <div class="floating-card card-1">
            <span class="card-icon">📊</span>
            <span class="card-text">Real-time Analysis</span>
          </div>
          
          <div class="floating-card card-2">
            <span class="card-icon">🎯</span>
            <span class="card-text">95% Accuracy</span>
          </div>
          
          <div class="floating-card card-3">
            <span class="card-icon">⚡</span>
            <span class="card-text">Instant Reports</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Trusted By Section -->
    <section class="trusted-by">
      <p class="trusted-label">Trusted by innovative teams worldwide</p>
      <div class="logo-strip">
        <div class="logo-item">TechCorp</div>
        <div class="logo-item">DataFlow</div>
        <div class="logo-item">AIVentures</div>
        <div class="logo-item">FutureLabs</div>
        <div class="logo-item">SmartScale</div>
      </div>
    </section>

    <!-- Features Section -->
    <section id="features" class="features">
      <div class="section-header">
        <span class="section-badge">Features</span>
        <h2 class="section-title">Everything you need to predict outcomes</h2>
        <p class="section-subtitle">
          Powerful tools designed to help you simulate, analyze, and make better decisions
        </p>
      </div>
      
      <div class="features-grid">
        <div class="feature-card">
          <div class="feature-icon">🧠</div>
          <h3 class="feature-title">Knowledge Graph Building</h3>
          <p class="feature-desc">
            Automatically extract entities and relationships from your documents to build comprehensive knowledge graphs.
          </p>
        </div>
        
        <div class="feature-card">
          <div class="feature-icon">👥</div>
          <h3 class="feature-title">Multi-Agent Simulation</h3>
          <p class="feature-desc">
            Deploy millions of AI agents that interact, debate, and simulate real-world social dynamics.
          </p>
        </div>
        
        <div class="feature-card">
          <div class="feature-icon">📈</div>
          <h3 class="feature-title">Predictive Analytics</h3>
          <p class="feature-desc">
            Get actionable insights and probability distributions for various outcome scenarios.
          </p>
        </div>
        
        <div class="feature-card">
          <div class="feature-icon">💬</div>
          <h3 class="feature-title">Deep Interaction</h3>
          <p class="feature-desc">
            Chat with any simulated agent or the Report Agent to explore insights in depth.
          </p>
        </div>
        
        <div class="feature-card">
          <div class="feature-icon">📄</div>
          <h3 class="feature-title">Automated Reports</h3>
          <p class="feature-desc">
            Generate comprehensive reports with visualizations, summaries, and recommendations.
          </p>
        </div>
        
        <div class="feature-card">
          <div class="feature-icon">🔒</div>
          <h3 class="feature-title">Enterprise Security</h3>
          <p class="feature-desc">
            Your data is encrypted and never shared. SOC 2 compliant infrastructure.
          </p>
        </div>
      </div>
    </section>

    <!-- How It Works Section -->
    <section id="how-it-works" class="how-it-works">
      <div class="section-header">
        <span class="section-badge">How It Works</span>
        <h2 class="section-title">From document to prediction in 5 steps</h2>
      </div>
      
      <div class="steps-timeline">
        <div class="step-item">
          <div class="step-number">01</div>
          <div class="step-content">
            <h3 class="step-title">Upload Documents</h3>
            <p class="step-desc">Upload PDFs, markdown, or text files containing the information you want to analyze.</p>
          </div>
        </div>
        
        <div class="step-item">
          <div class="step-number">02</div>
          <div class="step-content">
            <h3 class="step-title">Build Knowledge Graph</h3>
            <p class="step-desc">Our AI extracts entities, relationships, and context to create a comprehensive knowledge graph.</p>
          </div>
        </div>
        
        <div class="step-item">
          <div class="step-number">03</div>
          <div class="step-content">
            <h3 class="step-title">Configure Simulation</h3>
            <p class="step-desc">Set your prediction parameters and let AI agents populate the simulation environment.</p>
          </div>
        </div>
        
        <div class="step-item">
          <div class="step-number">04</div>
          <div class="step-content">
            <h3 class="step-title">Run Simulation</h3>
            <p class="step-desc">Watch as millions of agents interact, debate, and simulate real-world scenarios.</p>
          </div>
        </div>
        
        <div class="step-item">
          <div class="step-number">05</div>
          <div class="step-content">
            <h3 class="step-title">Get Insights</h3>
            <p class="step-desc">Receive detailed reports with predictions, probabilities, and actionable recommendations.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Pricing Section -->
    <section id="pricing" class="pricing">
      <div class="section-header">
        <span class="section-badge">Pricing</span>
        <h2 class="section-title">Simple, transparent pricing</h2>
        <p class="section-subtitle">Start free, scale as you grow</p>
      </div>
      
      <div class="pricing-toggle">
        <span :class="{ 'active': !isAnnual }">Monthly</span>
        <button class="toggle-btn" @click="isAnnual = !isAnnual" :class="{ 'annual': isAnnual }">
          <span class="toggle-slider"></span>
        </button>
        <span :class="{ 'active': isAnnual }">Annual <span class="save-badge">Save 20%</span></span>
      </div>
      
      <div class="pricing-grid">
        <div class="pricing-card">
          <div class="plan-header">
            <h3 class="plan-name">Starter</h3>
            <p class="plan-desc">Perfect for trying out Fish Predictions</p>
          </div>
          <div class="plan-price">
            <span class="price-currency">$</span>
            <span class="price-amount">0</span>
            <span class="price-period">/month</span>
          </div>
          <ul class="plan-features">
            <li><span class="check">✓</span> 3 simulations per month</li>
            <li><span class="check">✓</span> Up to 10,000 agents</li>
            <li><span class="check">✓</span> Basic reports</li>
            <li><span class="check">✓</span> Email support</li>
          </ul>
          <router-link to="/signup" class="btn-plan">Get Started Free</router-link>
        </div>
        
        <div class="pricing-card featured">
          <div class="popular-badge">Most Popular</div>
          <div class="plan-header">
            <h3 class="plan-name">Professional</h3>
            <p class="plan-desc">For teams and growing businesses</p>
          </div>
          <div class="plan-price">
            <span class="price-currency">$</span>
            <span class="price-amount">{{ isAnnual ? '79' : '99' }}</span>
            <span class="price-period">/month</span>
          </div>
          <ul class="plan-features">
            <li><span class="check">✓</span> Unlimited simulations</li>
            <li><span class="check">✓</span> Up to 1M agents</li>
            <li><span class="check">✓</span> Advanced reports & analytics</li>
            <li><span class="check">✓</span> Priority support</li>
            <li><span class="check">✓</span> API access</li>
            <li><span class="check">✓</span> Team collaboration</li>
          </ul>
          <router-link to="/signup?plan=pro" class="btn-plan primary">Start Free Trial</router-link>
        </div>
        
        <div class="pricing-card">
          <div class="plan-header">
            <h3 class="plan-name">Enterprise</h3>
            <p class="plan-desc">For large organizations</p>
          </div>
          <div class="plan-price">
            <span class="price-amount custom">Custom</span>
          </div>
          <ul class="plan-features">
            <li><span class="check">✓</span> Everything in Professional</li>
            <li><span class="check">✓</span> Unlimited agents</li>
            <li><span class="check">✓</span> Custom integrations</li>
            <li><span class="check">✓</span> Dedicated support</li>
            <li><span class="check">✓</span> SLA guarantee</li>
            <li><span class="check">✓</span> On-premise deployment</li>
          </ul>
          <a href="mailto:sales@fishpredictions.com" class="btn-plan">Contact Sales</a>
        </div>
      </div>
    </section>

    <!-- FAQ Section -->
    <section id="faq" class="faq">
      <div class="section-header">
        <span class="section-badge">FAQ</span>
        <h2 class="section-title">Frequently asked questions</h2>
      </div>
      
      <div class="faq-list">
        <div class="faq-item" v-for="(item, index) in faqItems" :key="index" :class="{ 'open': openFaq === index }">
          <button class="faq-question" @click="toggleFaq(index)">
            <span>{{ item.question }}</span>
            <span class="faq-icon">{{ openFaq === index ? '−' : '+' }}</span>
          </button>
          <div class="faq-answer" v-show="openFaq === index">
            <p>{{ item.answer }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="cta">
      <div class="cta-content">
        <h2 class="cta-title">Ready to predict the future?</h2>
        <p class="cta-subtitle">Join thousands of teams making better decisions with Fish Predictions</p>
        <div class="cta-actions">
          <router-link to="/signup" class="btn-primary large">
            Start Free Trial
            <span class="btn-arrow">→</span>
          </router-link>
          <a href="mailto:hello@fishpredictions.com" class="btn-secondary">Talk to Sales</a>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="footer-content">
        <div class="footer-brand">
          <div class="brand-logo">
            <span class="brand-icon">🐟</span>
            <span class="brand-text">Fish Predictions</span>
          </div>
          <p class="brand-tagline">Predict the future with swarm intelligence</p>
        </div>
        
        <div class="footer-links">
          <div class="link-group">
            <h4>Product</h4>
            <a href="#features">Features</a>
            <a href="#pricing">Pricing</a>
            <a href="#how-it-works">How It Works</a>
            <a href="#">API Docs</a>
          </div>
          
          <div class="link-group">
            <h4>Company</h4>
            <a href="#">About</a>
            <a href="#">Blog</a>
            <a href="#">Careers</a>
            <a href="#">Contact</a>
          </div>
          
          <div class="link-group">
            <h4>Legal</h4>
            <a href="#">Privacy Policy</a>
            <a href="#">Terms of Service</a>
            <a href="#">Cookie Policy</a>
          </div>
        </div>
      </div>
      
      <div class="footer-bottom">
        <p>&copy; 2024 Fish Predictions. All rights reserved.</p>
        <div class="social-links">
          <a href="#" class="social-link">Twitter</a>
          <a href="#" class="social-link">LinkedIn</a>
          <a href="#" class="social-link">GitHub</a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const mobileMenuOpen = ref(false)
const isAnnual = ref(true)
const openFaq = ref(null)

const faqItems = [
  {
    question: 'What types of documents can I upload?',
    answer: 'Fish Predictions supports PDF, Markdown (.md), and plain text (.txt) files. We can extract and analyze content from research papers, reports, articles, and any text-based documents.'
  },
  {
    question: 'How accurate are the predictions?',
    answer: 'Our multi-agent simulations achieve high accuracy by modeling complex social dynamics and interactions. The accuracy depends on the quality and completeness of your input data. Most users report 85-95% alignment with actual outcomes.'
  },
  {
    question: 'How long does a simulation take?',
    answer: 'Most simulations complete within 5-15 minutes, depending on the complexity and number of agents. You can monitor progress in real-time and interact with preliminary results as they become available.'
  },
  {
    question: 'Is my data secure?',
    answer: 'Absolutely. All data is encrypted in transit and at rest. We never share your data with third parties. Our infrastructure is SOC 2 compliant, and we offer data deletion upon request.'
  },
  {
    question: 'Can I integrate Fish Predictions with my existing tools?',
    answer: 'Yes! Professional and Enterprise plans include API access. You can integrate with your existing workflows, data pipelines, and business intelligence tools.'
  },
  {
    question: 'What happens after my free trial?',
    answer: 'After your 14-day free trial, you can choose to upgrade to a paid plan or continue with our free Starter plan with limited features. No credit card is required to start.'
  }
]

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const closeMobileMenu = () => {
  mobileMenuOpen.value = false
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const toggleFaq = (index) => {
  openFaq.value = openFaq.value === index ? null : index
}

const getAgentStyle = (i) => {
  const angle = (i / 12) * 2 * Math.PI
  const radius = 60 + Math.random() * 20
  const x = 100 + Math.cos(angle) * radius
  const y = 100 + Math.sin(angle) * radius
  return {
    left: `${x}px`,
    top: `${y}px`,
    animationDelay: `${i * 0.1}s`
  }
}
</script>

<style scoped>
/* Variables */
:root {
  --primary: #FF4500;
  --primary-dark: #E03E00;
  --black: #000000;
  --white: #FFFFFF;
  --gray-50: #F9FAFB;
  --gray-100: #F3F4F6;
  --gray-200: #E5E7EB;
  --gray-300: #D1D5DB;
  --gray-400: #9CA3AF;
  --gray-500: #6B7280;
  --gray-600: #4B5563;
  --gray-700: #374151;
  --gray-800: #1F2937;
  --gray-900: #111827;
}

* {
  box-sizing: border-box;
}

.landing-page {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  color: var(--gray-900);
  overflow-x: hidden;
}

/* Navbar */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--gray-200);
}

.nav-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 24px;
  height: 72px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-brand {
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
}

.brand-icon {
  font-size: 1.8rem;
}

.brand-text {
  font-weight: 700;
  font-size: 1.25rem;
  color: var(--gray-900);
}

.nav-links {
  display: flex;
  gap: 32px;
}

.nav-link {
  color: var(--gray-600);
  text-decoration: none;
  font-weight: 500;
  font-size: 0.95rem;
  transition: color 0.2s;
}

.nav-link:hover {
  color: var(--gray-900);
}

.nav-actions {
  display: flex;
  align-items: center;
  gap: 16px;
}

.btn-login {
  color: var(--gray-700);
  text-decoration: none;
  font-weight: 500;
  padding: 8px 16px;
  transition: color 0.2s;
}

.btn-login:hover {
  color: var(--gray-900);
}

.btn-signup {
  background: var(--primary);
  color: white;
  text-decoration: none;
  font-weight: 600;
  padding: 10px 20px;
  border-radius: 8px;
  transition: background 0.2s;
}

.btn-signup:hover {
  background: var(--primary-dark);
}

.mobile-menu-btn {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 5px;
}

.mobile-menu-btn span {
  width: 24px;
  height: 2px;
  background: var(--gray-700);
  transition: all 0.3s;
}

.mobile-menu {
  display: none;
  flex-direction: column;
  padding: 20px 24px;
  background: white;
  border-top: 1px solid var(--gray-200);
}

.mobile-menu.active {
  display: flex;
}

.mobile-link {
  padding: 12px 0;
  color: var(--gray-700);
  text-decoration: none;
  font-weight: 500;
  border-bottom: 1px solid var(--gray-100);
}

.mobile-actions {
  display: flex;
  flex-direction: column;
  gap: 12px;
  margin-top: 20px;
}

.mobile-actions .btn-login,
.mobile-actions .btn-signup {
  text-align: center;
}

/* Hero Section */
.hero {
  min-height: 100vh;
  padding: 120px 24px 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  inset: 0;
  z-index: -1;
}

.hero-gradient {
  position: absolute;
  inset: 0;
  background: radial-gradient(ellipse at 30% 20%, rgba(255, 69, 0, 0.08) 0%, transparent 50%),
              radial-gradient(ellipse at 70% 80%, rgba(255, 69, 0, 0.05) 0%, transparent 50%);
}

.hero-grid {
  position: absolute;
  inset: 0;
  background-image: 
    linear-gradient(rgba(0,0,0,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,0,0,0.03) 1px, transparent 1px);
  background-size: 60px 60px;
}

.hero-content {
  max-width: 600px;
  text-align: center;
  z-index: 1;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: var(--gray-100);
  padding: 8px 16px;
  border-radius: 100px;
  font-size: 0.875rem;
  font-weight: 500;
  color: var(--gray-700);
  margin-bottom: 24px;
}

.badge-icon {
  font-size: 1rem;
}

.hero-title {
  font-size: 3.5rem;
  font-weight: 700;
  line-height: 1.1;
  margin: 0 0 24px;
  letter-spacing: -0.02em;
}

.gradient-text {
  background: linear-gradient(135deg, var(--primary) 0%, #FF8C00 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  font-size: 1.25rem;
  color: var(--gray-600);
  line-height: 1.6;
  margin: 0 0 32px;
}

.hero-cta {
  display: flex;
  gap: 16px;
  justify-content: center;
  margin-bottom: 48px;
}

.btn-primary {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: var(--primary);
  color: white;
  text-decoration: none;
  font-weight: 600;
  padding: 14px 28px;
  border-radius: 10px;
  font-size: 1rem;
  transition: all 0.2s;
}

.btn-primary:hover {
  background: var(--primary-dark);
  transform: translateY(-2px);
}

.btn-primary.large {
  padding: 18px 36px;
  font-size: 1.1rem;
}

.btn-secondary {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: white;
  color: var(--gray-700);
  text-decoration: none;
  font-weight: 600;
  padding: 14px 28px;
  border-radius: 10px;
  font-size: 1rem;
  border: 1px solid var(--gray-300);
  transition: all 0.2s;
}

.btn-secondary:hover {
  border-color: var(--gray-400);
  background: var(--gray-50);
}

.play-icon {
  font-size: 0.75rem;
}

.hero-stats {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 32px;
}

.stat-item {
  text-align: center;
}

.stat-value {
  display: block;
  font-size: 1.75rem;
  font-weight: 700;
  color: var(--gray-900);
}

.stat-label {
  font-size: 0.875rem;
  color: var(--gray-500);
}

.stat-divider {
  width: 1px;
  height: 40px;
  background: var(--gray-300);
}

.hero-visual {
  position: absolute;
  right: -100px;
  top: 50%;
  transform: translateY(-50%);
  width: 500px;
  height: 400px;
  display: none;
}

.visual-container {
  position: relative;
  width: 100%;
  height: 100%;
}

.main-card {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 280px;
  height: 200px;
  background: white;
  border-radius: 16px;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.15);
  overflow: hidden;
}

.card-header {
  display: flex;
  gap: 6px;
  padding: 12px 16px;
  background: var(--gray-100);
}

.card-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}

.card-dot.green { background: #22C55E; }
.card-dot.yellow { background: #EAB308; }
.card-dot.red { background: #EF4444; }

.card-content {
  padding: 20px;
}

.simulation-preview {
  position: relative;
  width: 100%;
  height: 120px;
}

.agent-cluster {
  position: relative;
  width: 100%;
  height: 100%;
}

.agent {
  position: absolute;
  width: 12px;
  height: 12px;
  background: var(--primary);
  border-radius: 50%;
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { transform: scale(1); opacity: 0.8; }
  50% { transform: scale(1.2); opacity: 1; }
}

.floating-card {
  position: absolute;
  background: white;
  padding: 12px 16px;
  border-radius: 10px;
  box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 0.875rem;
  font-weight: 500;
}

.card-1 { top: 20px; left: 20px; }
.card-2 { bottom: 60px; left: 0; }
.card-3 { top: 80px; right: 0; }

/* Trusted By */
.trusted-by {
  padding: 60px 24px;
  background: var(--gray-50);
  text-align: center;
}

.trusted-label {
  font-size: 0.875rem;
  color: var(--gray-500);
  margin-bottom: 24px;
}

.logo-strip {
  display: flex;
  justify-content: center;
  gap: 48px;
  flex-wrap: wrap;
}

.logo-item {
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--gray-400);
}

/* Section Styles */
.section-header {
  text-align: center;
  margin-bottom: 60px;
}

.section-badge {
  display: inline-block;
  background: rgba(255, 69, 0, 0.1);
  color: var(--primary);
  padding: 6px 14px;
  border-radius: 100px;
  font-size: 0.875rem;
  font-weight: 600;
  margin-bottom: 16px;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin: 0 0 16px;
  letter-spacing: -0.02em;
}

.section-subtitle {
  font-size: 1.125rem;
  color: var(--gray-600);
  max-width: 600px;
  margin: 0 auto;
}

/* Features */
.features {
  padding: 100px 24px;
  max-width: 1280px;
  margin: 0 auto;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
}

.feature-card {
  padding: 32px;
  background: white;
  border: 1px solid var(--gray-200);
  border-radius: 16px;
  transition: all 0.3s;
}

.feature-card:hover {
  border-color: var(--primary);
  box-shadow: 0 10px 40px -10px rgba(255, 69, 0, 0.15);
  transform: translateY(-4px);
}

.feature-icon {
  font-size: 2.5rem;
  margin-bottom: 20px;
}

.feature-title {
  font-size: 1.25rem;
  font-weight: 600;
  margin: 0 0 12px;
}

.feature-desc {
  color: var(--gray-600);
  line-height: 1.6;
  margin: 0;
}

/* How It Works */
.how-it-works {
  padding: 100px 24px;
  background: var(--gray-50);
}

.steps-timeline {
  max-width: 800px;
  margin: 0 auto;
}

.step-item {
  display: flex;
  gap: 32px;
  padding: 32px 0;
  border-bottom: 1px solid var(--gray-200);
}

.step-item:last-child {
  border-bottom: none;
}

.step-number {
  font-size: 2rem;
  font-weight: 700;
  color: var(--primary);
  opacity: 0.3;
  min-width: 60px;
}

.step-title {
  font-size: 1.25rem;
  font-weight: 600;
  margin: 0 0 8px;
}

.step-desc {
  color: var(--gray-600);
  margin: 0;
  line-height: 1.6;
}

/* Pricing */
.pricing {
  padding: 100px 24px;
  max-width: 1280px;
  margin: 0 auto;
}

.pricing-toggle {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 16px;
  margin-bottom: 48px;
  font-weight: 500;
  color: var(--gray-500);
}

.pricing-toggle span.active {
  color: var(--gray-900);
}

.toggle-btn {
  width: 56px;
  height: 28px;
  background: var(--gray-200);
  border: none;
  border-radius: 100px;
  cursor: pointer;
  position: relative;
  transition: background 0.3s;
}

.toggle-btn.annual {
  background: var(--primary);
}

.toggle-slider {
  position: absolute;
  top: 3px;
  left: 3px;
  width: 22px;
  height: 22px;
  background: white;
  border-radius: 50%;
  transition: transform 0.3s;
}

.toggle-btn.annual .toggle-slider {
  transform: translateX(28px);
}

.save-badge {
  background: rgba(255, 69, 0, 0.1);
  color: var(--primary);
  padding: 2px 8px;
  border-radius: 100px;
  font-size: 0.75rem;
  margin-left: 4px;
}

.pricing-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
}

.pricing-card {
  background: white;
  border: 1px solid var(--gray-200);
  border-radius: 20px;
  padding: 40px;
  position: relative;
}

.pricing-card.featured {
  border: 2px solid var(--primary);
  transform: scale(1.05);
}

.popular-badge {
  position: absolute;
  top: -12px;
  left: 50%;
  transform: translateX(-50%);
  background: var(--primary);
  color: white;
  padding: 6px 16px;
  border-radius: 100px;
  font-size: 0.75rem;
  font-weight: 600;
}

.plan-header {
  margin-bottom: 24px;
}

.plan-name {
  font-size: 1.5rem;
  font-weight: 700;
  margin: 0 0 8px;
}

.plan-desc {
  color: var(--gray-500);
  margin: 0;
  font-size: 0.95rem;
}

.plan-price {
  margin-bottom: 32px;
}

.price-currency {
  font-size: 1.5rem;
  font-weight: 600;
  vertical-align: top;
}

.price-amount {
  font-size: 3.5rem;
  font-weight: 700;
  line-height: 1;
}

.price-amount.custom {
  font-size: 2rem;
}

.price-period {
  color: var(--gray-500);
}

.plan-features {
  list-style: none;
  padding: 0;
  margin: 0 0 32px;
}

.plan-features li {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 10px 0;
  color: var(--gray-700);
}

.check {
  color: var(--primary);
  font-weight: 700;
}

.btn-plan {
  display: block;
  text-align: center;
  padding: 14px 24px;
  border-radius: 10px;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.2s;
  background: var(--gray-100);
  color: var(--gray-700);
}

.btn-plan:hover {
  background: var(--gray-200);
}

.btn-plan.primary {
  background: var(--primary);
  color: white;
}

.btn-plan.primary:hover {
  background: var(--primary-dark);
}

/* FAQ */
.faq {
  padding: 100px 24px;
  background: var(--gray-50);
}

.faq-list {
  max-width: 800px;
  margin: 0 auto;
}

.faq-item {
  background: white;
  border: 1px solid var(--gray-200);
  border-radius: 12px;
  margin-bottom: 16px;
  overflow: hidden;
}

.faq-question {
  width: 100%;
  padding: 20px 24px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: none;
  border: none;
  cursor: pointer;
  font-size: 1rem;
  font-weight: 600;
  text-align: left;
  color: var(--gray-900);
}

.faq-icon {
  font-size: 1.5rem;
  color: var(--primary);
}

.faq-answer {
  padding: 0 24px 20px;
  color: var(--gray-600);
  line-height: 1.6;
}

/* CTA */
.cta {
  padding: 100px 24px;
  background: var(--gray-900);
  text-align: center;
}

.cta-title {
  font-size: 2.5rem;
  font-weight: 700;
  color: white;
  margin: 0 0 16px;
}

.cta-subtitle {
  font-size: 1.25rem;
  color: var(--gray-400);
  margin: 0 0 40px;
}

.cta-actions {
  display: flex;
  gap: 16px;
  justify-content: center;
}

.cta .btn-secondary {
  background: transparent;
  border-color: var(--gray-600);
  color: white;
}

.cta .btn-secondary:hover {
  border-color: white;
  background: rgba(255, 255, 255, 0.1);
}

/* Footer */
.footer {
  background: var(--gray-900);
  padding: 80px 24px 40px;
  color: var(--gray-400);
}

.footer-content {
  max-width: 1280px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  gap: 60px;
  margin-bottom: 60px;
}

.footer-brand {
  max-width: 300px;
}

.brand-logo {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 16px;
}

.brand-logo .brand-text {
  color: white;
}

.brand-tagline {
  margin: 0;
  line-height: 1.6;
}

.footer-links {
  display: flex;
  gap: 80px;
}

.link-group h4 {
  color: white;
  font-size: 0.875rem;
  font-weight: 600;
  margin: 0 0 20px;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.link-group a {
  display: block;
  color: var(--gray-400);
  text-decoration: none;
  padding: 8px 0;
  transition: color 0.2s;
}

.link-group a:hover {
  color: white;
}

.footer-bottom {
  max-width: 1280px;
  margin: 0 auto;
  padding-top: 40px;
  border-top: 1px solid var(--gray-800);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.footer-bottom p {
  margin: 0;
}

.social-links {
  display: flex;
  gap: 24px;
}

.social-link {
  color: var(--gray-400);
  text-decoration: none;
  transition: color 0.2s;
}

.social-link:hover {
  color: white;
}

/* Responsive */
@media (max-width: 1024px) {
  .hero-visual {
    display: none;
  }
  
  .features-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  
  .pricing-grid {
    grid-template-columns: 1fr;
    max-width: 400px;
    margin: 0 auto;
  }
  
  .pricing-card.featured {
    transform: none;
  }
  
  .footer-content {
    flex-direction: column;
  }
  
  .footer-links {
    flex-wrap: wrap;
    gap: 40px;
  }
}

@media (max-width: 768px) {
  .nav-links,
  .nav-actions {
    display: none;
  }
  
  .mobile-menu-btn {
    display: flex;
  }
  
  .hero-title {
    font-size: 2.5rem;
  }
  
  .hero-cta {
    flex-direction: column;
  }
  
  .hero-stats {
    flex-direction: column;
    gap: 24px;
  }
  
  .stat-divider {
    width: 60px;
    height: 1px;
  }
  
  .features-grid {
    grid-template-columns: 1fr;
  }
  
  .step-item {
    flex-direction: column;
    gap: 16px;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .footer-bottom {
    flex-direction: column;
    gap: 20px;
    text-align: center;
  }
}
</style>
