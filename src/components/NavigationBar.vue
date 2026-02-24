<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  activeTab: {
    type: String,
    default: 'home'
  }
})

const emit = defineEmits(['tab-change'])

const currentTab = ref(props.activeTab)

watch(() => props.activeTab, (newVal) => {
  currentTab.value = newVal
})

const tabs = [
  { id: 'home', label: '首页', icon: '🏠' },
  { id: 'about', label: '关于', icon: '💫' },
  { id: 'features', label: '功能', icon: '🛠️' },
  { id: 'contact', label: '联系', icon: '💬' }
]

const switchTab = (tabId) => {
  currentTab.value = tabId
  emit('tab-change', tabId)
}
</script>

<template>
  <nav class="navbar">
    <div class="navbar-container">
      <div class="navbar-brand">
        <span class="brand-icon">🤖</span>
        <span class="brand-text">AI 助手</span>
      </div>

      <div class="navbar-menu">
        <button
          v-for="tab in tabs"
          :key="tab.id"
          :class="['nav-item', { active: currentTab === tab.id }]"
          @click="switchTab(tab.id)"
        >
          <span class="nav-icon">{{ tab.icon }}</span>
          <span class="nav-label">{{ tab.label }}</span>
        </button>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  background: rgba(255, 255, 255, 0.98);
  backdrop-filter: blur(10px);
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
  position: sticky;
  top: 0;
  z-index: 1000;
}

.navbar-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 15px 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 15px;
}

.navbar-brand {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 1.3rem;
  font-weight: bold;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.brand-icon {
  font-size: 1.5rem;
}

.navbar-menu {
  display: flex;
  gap: 5px;
}

.nav-item {
  padding: 10px 20px;
  border: none;
  background: transparent;
  border-radius: 25px;
  cursor: pointer;
  font-size: 0.95rem;
  font-weight: 500;
  color: #666;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 6px;
}

.nav-item:hover {
  background: rgba(102, 126, 234, 0.1);
  color: #667eea;
  transform: translateY(-2px);
}

.nav-item.active {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
}

.nav-item.active:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.5);
}

.nav-icon {
  font-size: 1.1rem;
}

.nav-label {
  font-size: 0.9rem;
}

@media (max-width: 600px) {
  .navbar-container {
    padding: 12px 15px;
    flex-direction: column;
    gap: 12px;
  }

  .navbar-brand {
    font-size: 1.1rem;
    width: 100%;
    justify-content: center;
  }

  .navbar-menu {
    width: 100%;
    justify-content: space-between;
  }

  .nav-item {
    padding: 8px 12px;
    flex: 1;
    justify-content: center;
    flex-direction: column;
    gap: 4px;
  }

  .nav-label {
    font-size: 0.75rem;
  }

  .nav-icon {
    font-size: 1.2rem;
  }
}
</style>
