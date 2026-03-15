<template>
  <div class="auth-page">
    <div class="auth-container">
      <!-- Left Side - Branding -->
      <div class="auth-branding">
        <div class="brand-content">
          <router-link to="/" class="brand-logo">
            <span class="brand-icon">🐟</span>
            <span class="brand-text">Fish Predictions</span>
          </router-link>
          
          <h1 class="brand-headline">
            Predict the future with<br>
            <span class="gradient-text">Swarm Intelligence</span>
          </h1>
          
          <p class="brand-desc">
            Join thousands of teams making better decisions with AI-powered simulations.
          </p>
          
          <div class="testimonial">
            <p class="testimonial-text">
              "Fish Predictions helped us anticipate market changes 3 months in advance. Game changer for our strategy team."
            </p>
            <div class="testimonial-author">
              <div class="author-avatar">JD</div>
              <div class="author-info">
                <span class="author-name">John Doe</span>
                <span class="author-role">VP Strategy, TechCorp</span>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Right Side - Login Form -->
      <div class="auth-form-container">
        <div class="auth-form-wrapper">
          <div class="form-header">
            <h2>Welcome back</h2>
            <p>Enter your credentials to access your account</p>
          </div>
          
          <form @submit.prevent="handleLogin" class="auth-form">
            <div class="form-group">
              <label for="email">Email</label>
              <input 
                type="email" 
                id="email" 
                v-model="form.email"
                placeholder="Enter your email"
                required
                :disabled="loading"
              />
            </div>
            
            <div class="form-group">
              <label for="password">
                Password
                <router-link to="/forgot-password" class="forgot-link">Forgot password?</router-link>
              </label>
              <div class="password-input">
                <input 
                  :type="showPassword ? 'text' : 'password'" 
                  id="password" 
                  v-model="form.password"
                  placeholder="Enter your password"
                  required
                  :disabled="loading"
                />
                <button type="button" class="toggle-password" @click="showPassword = !showPassword">
                  {{ showPassword ? '👁️' : '👁️‍🗨️' }}
                </button>
              </div>
            </div>
            
            <div class="form-group checkbox-group">
              <label class="checkbox-label">
                <input type="checkbox" v-model="form.rememberMe" />
                <span class="checkmark"></span>
                Remember me for 30 days
              </label>
            </div>
            
            <div v-if="error" class="error-message">
              {{ error }}
            </div>
            
            <button type="submit" class="btn-submit" :disabled="loading">
              <span v-if="!loading">Sign In</span>
              <span v-else class="loading-spinner"></span>
            </button>
          </form>
          
          <div class="divider">
            <span>or continue with</span>
          </div>
          
          <div class="social-login">
            <button class="btn-social" @click="handleGoogleLogin">
              <svg viewBox="0 0 24 24" width="20" height="20">
                <path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/>
                <path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/>
                <path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z"/>
                <path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"/>
              </svg>
              Google
            </button>
            <button class="btn-social" @click="handleGithubLogin">
              <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor">
                <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
              </svg>
              GitHub
            </button>
          </div>
          
          <p class="auth-footer">
            Don't have an account? 
            <router-link to="/signup">Sign up for free</router-link>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const form = ref({
  email: '',
  password: '',
  rememberMe: false
})

const showPassword = ref(false)
const loading = ref(false)
const error = ref('')

const handleLogin = async () => {
  error.value = ''
  loading.value = true
  
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1500))
    
    // For demo: accept any credentials
    // In production, this would call your auth API
    localStorage.setItem('auth_token', 'demo_token_' + Date.now())
    localStorage.setItem('user', JSON.stringify({
      email: form.value.email,
      name: form.value.email.split('@')[0],
      plan: 'starter'
    }))
    
    router.push('/dashboard')
  } catch (err) {
    error.value = 'Invalid email or password. Please try again.'
  } finally {
    loading.value = false
  }
}

const handleGoogleLogin = () => {
  // In production, implement OAuth flow
  alert('Google OAuth integration coming soon!')
}

const handleGithubLogin = () => {
  // In production, implement OAuth flow
  alert('GitHub OAuth integration coming soon!')
}
</script>

<style scoped>
.auth-page {
  min-height: 100vh;
  background: #F9FAFB;
}

.auth-container {
  display: flex;
  min-height: 100vh;
}

/* Left Side - Branding */
.auth-branding {
  flex: 1;
  background: linear-gradient(135deg, #1F2937 0%, #111827 100%);
  padding: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.auth-branding::before {
  content: '';
  position: absolute;
  inset: 0;
  background: 
    radial-gradient(ellipse at 20% 30%, rgba(255, 69, 0, 0.15) 0%, transparent 50%),
    radial-gradient(ellipse at 80% 70%, rgba(255, 69, 0, 0.1) 0%, transparent 50%);
}

.brand-content {
  position: relative;
  z-index: 1;
  max-width: 480px;
  color: white;
}

.brand-logo {
  display: flex;
  align-items: center;
  gap: 12px;
  text-decoration: none;
  margin-bottom: 48px;
}

.brand-icon {
  font-size: 2.5rem;
}

.brand-text {
  font-size: 1.5rem;
  font-weight: 700;
  color: white;
}

.brand-headline {
  font-size: 2.75rem;
  font-weight: 700;
  line-height: 1.2;
  margin: 0 0 24px;
}

.gradient-text {
  background: linear-gradient(135deg, #FF4500 0%, #FF8C00 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.brand-desc {
  font-size: 1.125rem;
  color: #9CA3AF;
  line-height: 1.6;
  margin: 0 0 48px;
}

.testimonial {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  padding: 24px;
}

.testimonial-text {
  font-size: 1rem;
  line-height: 1.6;
  margin: 0 0 20px;
  color: #E5E7EB;
}

.testimonial-author {
  display: flex;
  align-items: center;
  gap: 12px;
}

.author-avatar {
  width: 44px;
  height: 44px;
  background: linear-gradient(135deg, #FF4500, #FF8C00);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
  font-size: 0.875rem;
}

.author-info {
  display: flex;
  flex-direction: column;
}

.author-name {
  font-weight: 600;
  color: white;
}

.author-role {
  font-size: 0.875rem;
  color: #9CA3AF;
}

/* Right Side - Form */
.auth-form-container {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 40px;
}

.auth-form-wrapper {
  width: 100%;
  max-width: 400px;
}

.form-header {
  margin-bottom: 32px;
}

.form-header h2 {
  font-size: 1.75rem;
  font-weight: 700;
  margin: 0 0 8px;
  color: #111827;
}

.form-header p {
  color: #6B7280;
  margin: 0;
}

.auth-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.form-group label {
  font-size: 0.875rem;
  font-weight: 500;
  color: #374151;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.forgot-link {
  color: #FF4500;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.875rem;
}

.forgot-link:hover {
  text-decoration: underline;
}

.form-group input[type="email"],
.form-group input[type="password"],
.form-group input[type="text"] {
  padding: 12px 16px;
  border: 1px solid #D1D5DB;
  border-radius: 10px;
  font-size: 1rem;
  transition: all 0.2s;
  background: white;
}

.form-group input:focus {
  outline: none;
  border-color: #FF4500;
  box-shadow: 0 0 0 3px rgba(255, 69, 0, 0.1);
}

.form-group input:disabled {
  background: #F3F4F6;
  cursor: not-allowed;
}

.password-input {
  position: relative;
}

.password-input input {
  width: 100%;
  padding-right: 48px;
}

.toggle-password {
  position: absolute;
  right: 12px;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  cursor: pointer;
  font-size: 1.1rem;
  opacity: 0.6;
}

.toggle-password:hover {
  opacity: 1;
}

.checkbox-group {
  flex-direction: row;
}

.checkbox-label {
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  font-size: 0.875rem;
  color: #4B5563;
}

.checkbox-label input {
  width: 18px;
  height: 18px;
  accent-color: #FF4500;
}

.error-message {
  background: #FEF2F2;
  border: 1px solid #FECACA;
  color: #DC2626;
  padding: 12px 16px;
  border-radius: 10px;
  font-size: 0.875rem;
}

.btn-submit {
  background: #FF4500;
  color: white;
  border: none;
  padding: 14px 24px;
  border-radius: 10px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 50px;
}

.btn-submit:hover:not(:disabled) {
  background: #E03E00;
  transform: translateY(-1px);
}

.btn-submit:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.loading-spinner {
  width: 20px;
  height: 20px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-top-color: white;
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.divider {
  display: flex;
  align-items: center;
  margin: 24px 0;
}

.divider::before,
.divider::after {
  content: '';
  flex: 1;
  height: 1px;
  background: #E5E7EB;
}

.divider span {
  padding: 0 16px;
  color: #9CA3AF;
  font-size: 0.875rem;
}

.social-login {
  display: flex;
  gap: 12px;
}

.btn-social {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding: 12px 20px;
  border: 1px solid #D1D5DB;
  border-radius: 10px;
  background: white;
  font-size: 0.95rem;
  font-weight: 500;
  color: #374151;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-social:hover {
  background: #F9FAFB;
  border-color: #9CA3AF;
}

.auth-footer {
  text-align: center;
  margin-top: 24px;
  color: #6B7280;
  font-size: 0.95rem;
}

.auth-footer a {
  color: #FF4500;
  text-decoration: none;
  font-weight: 600;
}

.auth-footer a:hover {
  text-decoration: underline;
}

/* Responsive */
@media (max-width: 1024px) {
  .auth-branding {
    display: none;
  }
  
  .auth-form-container {
    padding: 24px;
  }
}

@media (max-width: 480px) {
  .social-login {
    flex-direction: column;
  }
}
</style>
