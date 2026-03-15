<template>
  <div class="dashboard-layout">
    <!-- Sidebar -->
    <aside class="sidebar">
      <div class="sidebar-header">
        <router-link to="/" class="brand">
          <span class="brand-icon">🐟</span>
          <span class="brand-text">Fish Predictions</span>
        </router-link>
      </div>
      
      <nav class="sidebar-nav">
        <router-link to="/dashboard" class="nav-item" :class="{ active: currentTab === 'overview' }" @click="currentTab = 'overview'">
          <span class="nav-icon">📊</span>
          <span>Overview</span>
        </router-link>
        <router-link to="/dashboard" class="nav-item" :class="{ active: currentTab === 'simulations' }" @click="currentTab = 'simulations'">
          <span class="nav-icon">🔮</span>
          <span>Simulations</span>
        </router-link>
        <router-link to="/dashboard" class="nav-item" :class="{ active: currentTab === 'reports' }" @click="currentTab = 'reports'">
          <span class="nav-icon">📄</span>
          <span>Reports</span>
        </router-link>
        <router-link to="/dashboard" class="nav-item" :class="{ active: currentTab === 'api' }" @click="currentTab = 'api'">
          <span class="nav-icon">🔗</span>
          <span>API Keys</span>
        </router-link>
      </nav>
      
      <div class="sidebar-footer">
        <div class="usage-card">
          <div class="usage-header">
            <span class="usage-label">Monthly Usage</span>
            <span class="usage-value">{{ user?.plan === 'professional' ? 'Unlimited' : `${usageCount}/3` }}</span>
          </div>
          <div class="usage-bar" v-if="user?.plan !== 'professional'">
            <div class="usage-fill" :style="{ width: `${(usageCount / 3) * 100}%` }"></div>
          </div>
          <router-link to="/dashboard" class="upgrade-link" v-if="user?.plan === 'starter'" @click="currentTab = 'billing'">
            Upgrade Plan →
          </router-link>
        </div>
        
        <div class="user-menu">
          <div class="user-info" @click="showUserMenu = !showUserMenu">
            <div class="user-avatar">{{ userInitials }}</div>
            <div class="user-details">
              <span class="user-name">{{ user?.name || 'User' }}</span>
              <span class="user-plan">{{ planLabel }}</span>
            </div>
            <span class="menu-arrow">▾</span>
          </div>
          
          <div class="dropdown-menu" v-if="showUserMenu">
            <router-link to="/dashboard" class="dropdown-item" @click="currentTab = 'settings'">
              <span>⚙️</span> Settings
            </router-link>
            <router-link to="/dashboard" class="dropdown-item" @click="currentTab = 'billing'">
              <span>💳</span> Billing
            </router-link>
            <button class="dropdown-item" @click="handleLogout">
              <span>🚪</span> Log out
            </button>
          </div>
        </div>
      </div>
    </aside>
    
    <!-- Main Content -->
    <main class="main-content">
      <!-- Header -->
      <header class="content-header">
        <div class="header-left">
          <h1>{{ tabTitle }}</h1>
          <p class="header-subtitle">{{ tabSubtitle }}</p>
        </div>
        <div class="header-actions">
          <button class="btn-new" @click="startNewSimulation" v-if="currentTab === 'overview' || currentTab === 'simulations'">
            <span>+</span> New Simulation
          </button>
        </div>
      </header>
      
      <!-- Overview Tab -->
      <div v-if="currentTab === 'overview'" class="tab-content">
        <!-- Stats Cards -->
        <div class="stats-grid">
          <div class="stat-card">
            <div class="stat-icon">🔮</div>
            <div class="stat-info">
              <span class="stat-value">{{ stats.totalSimulations }}</span>
              <span class="stat-label">Total Simulations</span>
            </div>
          </div>
          <div class="stat-card">
            <div class="stat-icon">📄</div>
            <div class="stat-info">
              <span class="stat-value">{{ stats.totalReports }}</span>
              <span class="stat-label">Reports Generated</span>
            </div>
          </div>
          <div class="stat-card">
            <div class="stat-icon">👥</div>
            <div class="stat-info">
              <span class="stat-value">{{ formatNumber(stats.totalAgents) }}</span>
              <span class="stat-label">Agents Simulated</span>
            </div>
          </div>
          <div class="stat-card">
            <div class="stat-icon">⏱️</div>
            <div class="stat-info">
              <span class="stat-value">{{ stats.avgTime }}min</span>
              <span class="stat-label">Avg. Simulation Time</span>
            </div>
          </div>
        </div>
        
        <!-- Quick Actions -->
        <div class="section">
          <h2 class="section-title">Quick Actions</h2>
          <div class="quick-actions">
            <div class="action-card" @click="startNewSimulation">
              <div class="action-icon">🚀</div>
              <h3>New Simulation</h3>
              <p>Upload documents and start predicting</p>
            </div>
            <div class="action-card" @click="currentTab = 'reports'">
              <div class="action-icon">📊</div>
              <h3>View Reports</h3>
              <p>Access your generated reports</p>
            </div>
            <div class="action-card" @click="currentTab = 'api'">
              <div class="action-icon">🔑</div>
              <h3>API Access</h3>
              <p>Integrate with your applications</p>
            </div>
          </div>
        </div>
        
        <!-- Recent Activity -->
        <div class="section">
          <h2 class="section-title">Recent Activity</h2>
          <div class="activity-list" v-if="recentActivity.length">
            <div class="activity-item" v-for="activity in recentActivity" :key="activity.id">
              <div class="activity-icon" :class="activity.type">
                {{ activity.icon }}
              </div>
              <div class="activity-info">
                <span class="activity-title">{{ activity.title }}</span>
                <span class="activity-time">{{ activity.time }}</span>
              </div>
              <button class="activity-action" v-if="activity.actionLabel">
                {{ activity.actionLabel }}
              </button>
            </div>
          </div>
          <div class="empty-state" v-else>
            <div class="empty-icon">📭</div>
            <h3>No activity yet</h3>
            <p>Start your first simulation to see activity here</p>
            <button class="btn-primary" @click="startNewSimulation">Start Simulation</button>
          </div>
        </div>
      </div>
      
      <!-- Simulations Tab -->
      <div v-if="currentTab === 'simulations'" class="tab-content">
        <div class="simulations-list" v-if="simulations.length">
          <div class="simulation-card" v-for="sim in simulations" :key="sim.id">
            <div class="sim-header">
              <h3 class="sim-title">{{ sim.name }}</h3>
              <span class="sim-status" :class="sim.status">{{ sim.status }}</span>
            </div>
            <p class="sim-desc">{{ sim.requirement }}</p>
            <div class="sim-meta">
              <span><strong>Agents:</strong> {{ formatNumber(sim.agents) }}</span>
              <span><strong>Created:</strong> {{ sim.createdAt }}</span>
            </div>
            <div class="sim-actions">
              <button class="btn-outline" @click="viewSimulation(sim.id)">View Details</button>
              <button class="btn-outline" v-if="sim.reportId">View Report</button>
            </div>
          </div>
        </div>
        <div class="empty-state" v-else>
          <div class="empty-icon">🔮</div>
          <h3>No simulations yet</h3>
          <p>Create your first simulation to start predicting outcomes</p>
          <button class="btn-primary" @click="startNewSimulation">Create Simulation</button>
        </div>
      </div>
      
      <!-- Reports Tab -->
      <div v-if="currentTab === 'reports'" class="tab-content">
        <div class="empty-state">
          <div class="empty-icon">📄</div>
          <h3>No reports yet</h3>
          <p>Complete a simulation to generate your first report</p>
          <button class="btn-primary" @click="startNewSimulation">Start Simulation</button>
        </div>
      </div>
      
      <!-- API Keys Tab -->
      <div v-if="currentTab === 'api'" class="tab-content">
        <div class="api-section">
          <div class="api-header">
            <h2>API Keys</h2>
            <button class="btn-primary" @click="generateApiKey" :disabled="user?.plan === 'starter'">
              Generate New Key
            </button>
          </div>
          
          <div class="api-notice" v-if="user?.plan === 'starter'">
            <span class="notice-icon">ℹ️</span>
            <p>API access is available on Professional and Enterprise plans. <router-link to="/dashboard" @click="currentTab = 'billing'">Upgrade now</router-link></p>
          </div>
          
          <div class="api-keys-list" v-if="apiKeys.length">
            <div class="api-key-item" v-for="key in apiKeys" :key="key.id">
              <div class="key-info">
                <span class="key-name">{{ key.name }}</span>
                <code class="key-value">{{ key.masked }}</code>
              </div>
              <div class="key-meta">
                <span>Created: {{ key.createdAt }}</span>
                <span>Last used: {{ key.lastUsed || 'Never' }}</span>
              </div>
              <button class="btn-danger-outline" @click="revokeApiKey(key.id)">Revoke</button>
            </div>
          </div>
          
          <div class="api-docs">
            <h3>Quick Start</h3>
            <pre><code>curl -X POST https://api.fishpredictions.com/v1/simulate \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"requirement": "Your prediction query"}'</code></pre>
            <a href="#" class="docs-link">View full API documentation →</a>
          </div>
        </div>
      </div>
      
      <!-- Settings Tab -->
      <div v-if="currentTab === 'settings'" class="tab-content">
        <div class="settings-section">
          <h2>Profile Settings</h2>
          <form class="settings-form" @submit.prevent="saveSettings">
            <div class="form-group">
              <label>Full Name</label>
              <input type="text" v-model="settings.name" />
            </div>
            <div class="form-group">
              <label>Email</label>
              <input type="email" v-model="settings.email" />
            </div>
            <div class="form-group">
              <label>Company</label>
              <input type="text" v-model="settings.company" placeholder="Optional" />
            </div>
            <button type="submit" class="btn-primary">Save Changes</button>
          </form>
        </div>
        
        <div class="settings-section">
          <h2>Change Password</h2>
          <form class="settings-form" @submit.prevent="changePassword">
            <div class="form-group">
              <label>Current Password</label>
              <input type="password" v-model="passwordForm.current" />
            </div>
            <div class="form-group">
              <label>New Password</label>
              <input type="password" v-model="passwordForm.new" />
            </div>
            <div class="form-group">
              <label>Confirm New Password</label>
              <input type="password" v-model="passwordForm.confirm" />
            </div>
            <button type="submit" class="btn-primary">Update Password</button>
          </form>
        </div>
        
        <div class="settings-section danger-zone">
          <h2>Danger Zone</h2>
          <p>Once you delete your account, there is no going back. Please be certain.</p>
          <button class="btn-danger" @click="deleteAccount">Delete Account</button>
        </div>
      </div>
      
      <!-- Billing Tab -->
      <div v-if="currentTab === 'billing'" class="tab-content">
        <div class="billing-section">
          <div class="current-plan">
            <div class="plan-info">
              <h2>Current Plan</h2>
              <div class="plan-badge" :class="user?.plan">{{ planLabel }}</div>
            </div>
            <p class="plan-desc">{{ planDescription }}</p>
          </div>
          
          <div class="plans-grid">
            <div class="plan-card" :class="{ current: user?.plan === 'starter' }">
              <h3>Starter</h3>
              <div class="plan-price">
                <span class="price">$0</span>
                <span class="period">/month</span>
              </div>
              <ul class="plan-features">
                <li>3 simulations/month</li>
                <li>Up to 10,000 agents</li>
                <li>Basic reports</li>
                <li>Email support</li>
              </ul>
              <button class="btn-outline" disabled v-if="user?.plan === 'starter'">Current Plan</button>
              <button class="btn-outline" v-else @click="changePlan('starter')">Downgrade</button>
            </div>
            
            <div class="plan-card featured" :class="{ current: user?.plan === 'professional' }">
              <div class="popular-tag">Most Popular</div>
              <h3>Professional</h3>
              <div class="plan-price">
                <span class="price">$99</span>
                <span class="period">/month</span>
              </div>
              <ul class="plan-features">
                <li>Unlimited simulations</li>
                <li>Up to 1M agents</li>
                <li>Advanced reports</li>
                <li>Priority support</li>
                <li>API access</li>
                <li>Team collaboration</li>
              </ul>
              <button class="btn-primary" v-if="user?.plan === 'starter'" @click="upgradePlan">Upgrade Now</button>
              <button class="btn-outline" disabled v-else>Current Plan</button>
            </div>
            
            <div class="plan-card">
              <h3>Enterprise</h3>
              <div class="plan-price">
                <span class="price">Custom</span>
              </div>
              <ul class="plan-features">
                <li>Everything in Pro</li>
                <li>Unlimited agents</li>
                <li>Custom integrations</li>
                <li>Dedicated support</li>
                <li>SLA guarantee</li>
                <li>On-premise option</li>
              </ul>
              <button class="btn-outline" @click="contactSales">Contact Sales</button>
            </div>
          </div>
          
          <div class="billing-history" v-if="user?.plan !== 'starter'">
            <h2>Billing History</h2>
            <table class="billing-table">
              <thead>
                <tr>
                  <th>Date</th>
                  <th>Description</th>
                  <th>Amount</th>
                  <th>Status</th>
                  <th></th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td>Mar 1, 2024</td>
                  <td>Professional Plan - Monthly</td>
                  <td>$99.00</td>
                  <td><span class="status-badge paid">Paid</span></td>
                  <td><a href="#">Invoice</a></td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const currentTab = ref('overview')
const showUserMenu = ref(false)
const usageCount = ref(1)

const user = ref(null)
const settings = ref({ name: '', email: '', company: '' })
const passwordForm = ref({ current: '', new: '', confirm: '' })

const stats = ref({
  totalSimulations: 0,
  totalReports: 0,
  totalAgents: 0,
  avgTime: 0
})

const recentActivity = ref([])
const simulations = ref([])
const apiKeys = ref([])

const userInitials = computed(() => {
  if (!user.value?.name) return 'U'
  return user.value.name.split(' ').map(n => n[0]).join('').toUpperCase().slice(0, 2)
})

const planLabel = computed(() => {
  const plans = {
    starter: 'Starter',
    professional: 'Professional',
    enterprise: 'Enterprise'
  }
  return plans[user.value?.plan] || 'Starter'
})

const planDescription = computed(() => {
  const descriptions = {
    starter: 'Free plan with 3 simulations per month',
    professional: 'Unlimited simulations with advanced features',
    enterprise: 'Custom enterprise solution'
  }
  return descriptions[user.value?.plan] || descriptions.starter
})

const tabTitle = computed(() => {
  const titles = {
    overview: 'Dashboard',
    simulations: 'Simulations',
    reports: 'Reports',
    api: 'API Keys',
    settings: 'Settings',
    billing: 'Billing'
  }
  return titles[currentTab.value] || 'Dashboard'
})

const tabSubtitle = computed(() => {
  const subtitles = {
    overview: 'Welcome back! Here\'s what\'s happening with your predictions.',
    simulations: 'Manage and view all your simulations',
    reports: 'Access your generated prediction reports',
    api: 'Manage your API keys for programmatic access',
    settings: 'Manage your account settings',
    billing: 'Manage your subscription and billing'
  }
  return subtitles[currentTab.value] || ''
})

const formatNumber = (num) => {
  if (num >= 1000000) return (num / 1000000).toFixed(1) + 'M'
  if (num >= 1000) return (num / 1000).toFixed(1) + 'K'
  return num.toString()
}

const startNewSimulation = () => {
  router.push('/app')
}

const viewSimulation = (id) => {
  router.push(`/process/${id}`)
}

const generateApiKey = () => {
  alert('API key generation coming soon!')
}

const revokeApiKey = (id) => {
  if (confirm('Are you sure you want to revoke this API key?')) {
    apiKeys.value = apiKeys.value.filter(k => k.id !== id)
  }
}

const saveSettings = () => {
  alert('Settings saved!')
}

const changePassword = () => {
  if (passwordForm.value.new !== passwordForm.value.confirm) {
    alert('Passwords do not match')
    return
  }
  alert('Password updated!')
  passwordForm.value = { current: '', new: '', confirm: '' }
}

const deleteAccount = () => {
  if (confirm('Are you sure you want to delete your account? This action cannot be undone.')) {
    localStorage.removeItem('auth_token')
    localStorage.removeItem('user')
    router.push('/')
  }
}

const upgradePlan = () => {
  alert('Stripe integration coming soon! For now, your plan has been upgraded.')
  user.value.plan = 'professional'
  localStorage.setItem('user', JSON.stringify(user.value))
}

const changePlan = (plan) => {
  user.value.plan = plan
  localStorage.setItem('user', JSON.stringify(user.value))
}

const contactSales = () => {
  window.location.href = 'mailto:sales@fishpredictions.com'
}

const handleLogout = () => {
  localStorage.removeItem('auth_token')
  localStorage.removeItem('user')
  router.push('/')
}

onMounted(() => {
  // Check auth
  const token = localStorage.getItem('auth_token')
  if (!token) {
    router.push('/login')
    return
  }
  
  // Load user
  const userData = localStorage.getItem('user')
  if (userData) {
    user.value = JSON.parse(userData)
    settings.value.name = user.value.name
    settings.value.email = user.value.email
  }
  
  // Load demo data
  stats.value = {
    totalSimulations: 12,
    totalReports: 8,
    totalAgents: 2450000,
    avgTime: 8
  }
  
  recentActivity.value = [
    { id: 1, type: 'simulation', icon: '🔮', title: 'Simulation completed: Market Analysis Q1', time: '2 hours ago', actionLabel: 'View' },
    { id: 2, type: 'report', icon: '📄', title: 'Report generated: Product Launch Prediction', time: '1 day ago', actionLabel: 'Download' },
    { id: 3, type: 'simulation', icon: '🔮', title: 'New simulation started: Competitor Analysis', time: '2 days ago', actionLabel: 'View' }
  ]
  
  simulations.value = [
    { id: 'sim-1', name: 'Market Analysis Q1', requirement: 'Predict market trends for Q1 2024', agents: 500000, status: 'completed', createdAt: 'Mar 10, 2024', reportId: 'rep-1' },
    { id: 'sim-2', name: 'Product Launch', requirement: 'Simulate customer response to new product launch', agents: 1000000, status: 'completed', createdAt: 'Mar 8, 2024', reportId: 'rep-2' }
  ]
})
</script>

<style scoped>
.dashboard-layout {
  display: flex;
  min-height: 100vh;
  background: #F9FAFB;
}

/* Sidebar */
.sidebar {
  width: 280px;
  background: #1F2937;
  color: white;
  display: flex;
  flex-direction: column;
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  z-index: 100;
}

.sidebar-header {
  padding: 24px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.brand {
  display: flex;
  align-items: center;
  gap: 12px;
  text-decoration: none;
}

.brand-icon {
  font-size: 1.75rem;
}

.brand-text {
  font-size: 1.25rem;
  font-weight: 700;
  color: white;
}

.sidebar-nav {
  flex: 1;
  padding: 16px 12px;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  color: #9CA3AF;
  text-decoration: none;
  border-radius: 8px;
  margin-bottom: 4px;
  transition: all 0.2s;
}

.nav-item:hover {
  background: rgba(255, 255, 255, 0.05);
  color: white;
}

.nav-item.active {
  background: rgba(255, 69, 0, 0.2);
  color: #FF4500;
}

.nav-icon {
  font-size: 1.25rem;
}

.sidebar-footer {
  padding: 16px;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.usage-card {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 10px;
  padding: 16px;
  margin-bottom: 16px;
}

.usage-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
}

.usage-label {
  font-size: 0.875rem;
  color: #9CA3AF;
}

.usage-value {
  font-weight: 600;
  color: white;
}

.usage-bar {
  height: 4px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 2px;
  overflow: hidden;
  margin-bottom: 12px;
}

.usage-fill {
  height: 100%;
  background: #FF4500;
  transition: width 0.3s;
}

.upgrade-link {
  color: #FF4500;
  font-size: 0.875rem;
  text-decoration: none;
  font-weight: 500;
}

.upgrade-link:hover {
  text-decoration: underline;
}

.user-menu {
  position: relative;
}

.user-info {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px;
  border-radius: 10px;
  cursor: pointer;
  transition: background 0.2s;
}

.user-info:hover {
  background: rgba(255, 255, 255, 0.05);
}

.user-avatar {
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, #FF4500, #FF8C00);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
  font-size: 0.875rem;
}

.user-details {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.user-name {
  font-weight: 500;
  font-size: 0.95rem;
}

.user-plan {
  font-size: 0.75rem;
  color: #9CA3AF;
}

.menu-arrow {
  color: #9CA3AF;
}

.dropdown-menu {
  position: absolute;
  bottom: 100%;
  left: 0;
  right: 0;
  background: #374151;
  border-radius: 10px;
  padding: 8px;
  margin-bottom: 8px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
}

.dropdown-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 12px;
  color: #E5E7EB;
  text-decoration: none;
  border-radius: 6px;
  border: none;
  background: none;
  width: 100%;
  font-size: 0.95rem;
  cursor: pointer;
  transition: background 0.2s;
}

.dropdown-item:hover {
  background: rgba(255, 255, 255, 0.1);
}

/* Main Content */
.main-content {
  flex: 1;
  margin-left: 280px;
  padding: 32px;
}

.content-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 32px;
}

.content-header h1 {
  font-size: 1.75rem;
  font-weight: 700;
  margin: 0 0 4px;
  color: #111827;
}

.header-subtitle {
  color: #6B7280;
  margin: 0;
}

.btn-new {
  display: flex;
  align-items: center;
  gap: 8px;
  background: #FF4500;
  color: white;
  border: none;
  padding: 12px 20px;
  border-radius: 10px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-new:hover {
  background: #E03E00;
  transform: translateY(-1px);
}

/* Stats Grid */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  margin-bottom: 32px;
}

.stat-card {
  background: white;
  border: 1px solid #E5E7EB;
  border-radius: 12px;
  padding: 24px;
  display: flex;
  align-items: center;
  gap: 16px;
}

.stat-icon {
  font-size: 2rem;
}

.stat-info {
  display: flex;
  flex-direction: column;
}

.stat-value {
  font-size: 1.5rem;
  font-weight: 700;
  color: #111827;
}

.stat-label {
  font-size: 0.875rem;
  color: #6B7280;
}

/* Sections */
.section {
  margin-bottom: 32px;
}

.section-title {
  font-size: 1.25rem;
  font-weight: 600;
  margin: 0 0 16px;
  color: #111827;
}

/* Quick Actions */
.quick-actions {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

.action-card {
  background: white;
  border: 1px solid #E5E7EB;
  border-radius: 12px;
  padding: 24px;
  cursor: pointer;
  transition: all 0.2s;
}

.action-card:hover {
  border-color: #FF4500;
  box-shadow: 0 4px 12px rgba(255, 69, 0, 0.1);
  transform: translateY(-2px);
}

.action-icon {
  font-size: 2rem;
  margin-bottom: 12px;
}

.action-card h3 {
  font-size: 1rem;
  font-weight: 600;
  margin: 0 0 8px;
  color: #111827;
}

.action-card p {
  font-size: 0.875rem;
  color: #6B7280;
  margin: 0;
}

/* Activity List */
.activity-list {
  background: white;
  border: 1px solid #E5E7EB;
  border-radius: 12px;
  overflow: hidden;
}

.activity-item {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 16px 20px;
  border-bottom: 1px solid #F3F4F6;
}

.activity-item:last-child {
  border-bottom: none;
}

.activity-icon {
  width: 40px;
  height: 40px;
  background: #F3F4F6;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.25rem;
}

.activity-info {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.activity-title {
  font-weight: 500;
  color: #111827;
}

.activity-time {
  font-size: 0.875rem;
  color: #9CA3AF;
}

.activity-action {
  background: none;
  border: 1px solid #E5E7EB;
  padding: 8px 16px;
  border-radius: 6px;
  font-size: 0.875rem;
  color: #374151;
  cursor: pointer;
  transition: all 0.2s;
}

.activity-action:hover {
  border-color: #FF4500;
  color: #FF4500;
}

/* Empty State */
.empty-state {
  background: white;
  border: 1px solid #E5E7EB;
  border-radius: 12px;
  padding: 60px 40px;
  text-align: center;
}

.empty-icon {
  font-size: 3rem;
  margin-bottom: 16px;
}

.empty-state h3 {
  font-size: 1.25rem;
  font-weight: 600;
  margin: 0 0 8px;
  color: #111827;
}

.empty-state p {
  color: #6B7280;
  margin: 0 0 24px;
}

.btn-primary {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: #FF4500;
  color: white;
  border: none;
  padding: 12px 24px;
  border-radius: 10px;
  font-weight: 600;
  cursor: pointer;
  text-decoration: none;
  transition: all 0.2s;
}

.btn-primary:hover {
  background: #E03E00;
}

.btn-outline {
  background: white;
  border: 1px solid #E5E7EB;
  padding: 10px 20px;
  border-radius: 8px;
  font-weight: 500;
  color: #374151;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-outline:hover:not(:disabled) {
  border-color: #FF4500;
  color: #FF4500;
}

.btn-outline:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

/* Simulations */
.simulations-list {
  display: grid;
  gap: 20px;
}

.simulation-card {
  background: white;
  border: 1px solid #E5E7EB;
  border-radius: 12px;
  padding: 24px;
}

.sim-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;
}

.sim-title {
  font-size: 1.125rem;
  font-weight: 600;
  margin: 0;
  color: #111827;
}

.sim-status {
  padding: 4px 12px;
  border-radius: 100px;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: capitalize;
}

.sim-status.completed {
  background: #D1FAE5;
  color: #059669;
}

.sim-status.running {
  background: #FEF3C7;
  color: #D97706;
}

.sim-status.failed {
  background: #FEE2E2;
  color: #DC2626;
}

.sim-desc {
  color: #6B7280;
  margin: 0 0 16px;
}

.sim-meta {
  display: flex;
  gap: 24px;
  font-size: 0.875rem;
  color: #6B7280;
  margin-bottom: 16px;
}

.sim-actions {
  display: flex;
  gap: 12px;
}

/* API Section */
.api-section {
  background: white;
  border: 1px solid #E5E7EB;
  border-radius: 12px;
  padding: 24px;
}

.api-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
}

.api-header h2 {
  margin: 0;
  font-size: 1.25rem;
}

.api-notice {
  display: flex;
  align-items: center;
  gap: 12px;
  background: #FEF3C7;
  border: 1px solid #FCD34D;
  border-radius: 10px;
  padding: 16px;
  margin-bottom: 24px;
}

.api-notice p {
  margin: 0;
  color: #92400E;
}

.api-notice a {
  color: #D97706;
  font-weight: 600;
}

.api-keys-list {
  margin-bottom: 24px;
}

.api-key-item {
  display: flex;
  align-items: center;
  gap: 20px;
  padding: 16px;
  border: 1px solid #E5E7EB;
  border-radius: 10px;
  margin-bottom: 12px;
}

.key-info {
  flex: 1;
}

.key-name {
  display: block;
  font-weight: 500;
  margin-bottom: 4px;
}

.key-value {
  font-size: 0.875rem;
  color: #6B7280;
  background: #F3F4F6;
  padding: 4px 8px;
  border-radius: 4px;
}

.key-meta {
  display: flex;
  flex-direction: column;
  font-size: 0.75rem;
  color: #9CA3AF;
}

.btn-danger-outline {
  background: none;
  border: 1px solid #FCA5A5;
  color: #DC2626;
  padding: 8px 16px;
  border-radius: 6px;
  font-size: 0.875rem;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-danger-outline:hover {
  background: #FEE2E2;
}

.api-docs {
  background: #1F2937;
  border-radius: 10px;
  padding: 24px;
}

.api-docs h3 {
  color: white;
  margin: 0 0 16px;
  font-size: 1rem;
}

.api-docs pre {
  background: #111827;
  border-radius: 8px;
  padding: 16px;
  overflow-x: auto;
  margin: 0 0 16px;
}

.api-docs code {
  color: #E5E7EB;
  font-size: 0.875rem;
}

.docs-link {
  color: #FF4500;
  text-decoration: none;
  font-weight: 500;
}

.docs-link:hover {
  text-decoration: underline;
}

/* Settings */
.settings-section {
  background: white;
  border: 1px solid #E5E7EB;
  border-radius: 12px;
  padding: 24px;
  margin-bottom: 24px;
}

.settings-section h2 {
  font-size: 1.25rem;
  margin: 0 0 20px;
}

.settings-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-width: 400px;
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
}

.form-group input {
  padding: 12px 16px;
  border: 1px solid #D1D5DB;
  border-radius: 10px;
  font-size: 1rem;
  transition: all 0.2s;
}

.form-group input:focus {
  outline: none;
  border-color: #FF4500;
  box-shadow: 0 0 0 3px rgba(255, 69, 0, 0.1);
}

.danger-zone {
  border-color: #FCA5A5;
}

.danger-zone h2 {
  color: #DC2626;
}

.danger-zone p {
  color: #6B7280;
  margin: 0 0 20px;
}

.btn-danger {
  background: #DC2626;
  color: white;
  border: none;
  padding: 12px 24px;
  border-radius: 10px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-danger:hover {
  background: #B91C1C;
}

/* Billing */
.billing-section {
  display: flex;
  flex-direction: column;
  gap: 32px;
}

.current-plan {
  background: white;
  border: 1px solid #E5E7EB;
  border-radius: 12px;
  padding: 24px;
}

.plan-info {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-bottom: 8px;
}

.plan-info h2 {
  margin: 0;
  font-size: 1.25rem;
}

.plan-badge {
  padding: 4px 12px;
  border-radius: 100px;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: capitalize;
}

.plan-badge.starter {
  background: #E5E7EB;
  color: #374151;
}

.plan-badge.professional {
  background: #DBEAFE;
  color: #1D4ED8;
}

.plan-badge.enterprise {
  background: #F3E8FF;
  color: #7C3AED;
}

.plan-desc {
  color: #6B7280;
  margin: 0;
}

.plans-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

.plan-card {
  background: white;
  border: 1px solid #E5E7EB;
  border-radius: 16px;
  padding: 32px;
  position: relative;
}

.plan-card.featured {
  border: 2px solid #FF4500;
}

.plan-card.current {
  background: #FFF7ED;
}

.popular-tag {
  position: absolute;
  top: -12px;
  left: 50%;
  transform: translateX(-50%);
  background: #FF4500;
  color: white;
  padding: 4px 16px;
  border-radius: 100px;
  font-size: 0.75rem;
  font-weight: 600;
}

.plan-card h3 {
  font-size: 1.25rem;
  margin: 0 0 16px;
}

.plan-price {
  margin-bottom: 24px;
}

.plan-price .price {
  font-size: 2.5rem;
  font-weight: 700;
}

.plan-price .period {
  color: #6B7280;
}

.plan-features {
  list-style: none;
  padding: 0;
  margin: 0 0 24px;
}

.plan-features li {
  padding: 8px 0;
  color: #4B5563;
  display: flex;
  align-items: center;
  gap: 8px;
}

.plan-features li::before {
  content: '✓';
  color: #22C55E;
  font-weight: 700;
}

.billing-history {
  background: white;
  border: 1px solid #E5E7EB;
  border-radius: 12px;
  padding: 24px;
}

.billing-history h2 {
  margin: 0 0 20px;
  font-size: 1.25rem;
}

.billing-table {
  width: 100%;
  border-collapse: collapse;
}

.billing-table th,
.billing-table td {
  padding: 12px;
  text-align: left;
  border-bottom: 1px solid #E5E7EB;
}

.billing-table th {
  font-weight: 500;
  color: #6B7280;
  font-size: 0.875rem;
}

.status-badge {
  padding: 4px 12px;
  border-radius: 100px;
  font-size: 0.75rem;
  font-weight: 600;
}

.status-badge.paid {
  background: #D1FAE5;
  color: #059669;
}

.billing-table a {
  color: #FF4500;
  text-decoration: none;
}

.billing-table a:hover {
  text-decoration: underline;
}

/* Responsive */
@media (max-width: 1200px) {
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  
  .quick-actions {
    grid-template-columns: repeat(2, 1fr);
  }
  
  .plans-grid {
    grid-template-columns: 1fr;
    max-width: 400px;
  }
}

@media (max-width: 768px) {
  .sidebar {
    display: none;
  }
  
  .main-content {
    margin-left: 0;
    padding: 20px;
  }
  
  .stats-grid {
    grid-template-columns: 1fr;
  }
  
  .quick-actions {
    grid-template-columns: 1fr;
  }
  
  .content-header {
    flex-direction: column;
    gap: 16px;
  }
}
</style>
