<template>
  <div class="bg-white">
    <!-- Hero Banner Component -->
    <div class="relative min-h-screen bg-gray-100 overflow-hidden">
      <!-- Background Image -->
      <div class="absolute inset-0 overflow-hidden">
        <img 
          src="https://lotusoutreachaustralia.org.au/wp-content/uploads/2020/03/Bondi-BH-Class-Donation-Poster.jpg"
          alt="Lotus Outreach activities" 
          class="w-full h-full object-cover blur-sm"
        >
        <div class="absolute inset-0 bg-black/10"></div>
      </div>
      
      <!-- Content Overlay -->
      <div class="relative z-10 flex items-center justify-center min-h-screen px-4 sm:px-6 lg:px-8">
        <div class="text-center max-w-3xl mx-auto">
          <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold text-white mb-4 leading-tight">
            <span class="inline-block transform transition-all duration-500 hover:scale-105">
              Empowering Communities
            </span>
            <br>
            <span class="inline-block transition-all duration-300 text-pink-400">
              Through Sustainable Action
            </span>
          </h1>
          <p class="text-lg md:text-xl text-white mb-8 max-w-2xl mx-auto">
            Discover our ongoing activities and initiatives creating lasting change through education, sports, and community development worldwide.
          </p>
          <div class="flex flex-wrap justify-center gap-4">
            <button class="px-6 py-3 bg-pink-500 text-white font-medium rounded-full transition-all duration-300 shadow-lg hover:shadow-xl transform hover:-translate-y-1">
              Our Programs
            </button>
            <button class="px-6 py-3 border-2 border-white text-white font-medium rounded-full hover:bg-white hover:text-gray-900 transition-all duration-300 transform hover:-translate-y-1">
              Get Involved
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Activities Listing View -->
    <div v-if="currentView === 'listing'" class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16">
      <!-- Header with Search -->
      <div class="text-center mb-12">
        <h2 class="text-3xl md:text-4xl font-bold text-gray-900 mb-3">Our Activities</h2>
        <p class="text-lg text-gray-600 max-w-2xl mx-auto mb-6">
          Explore our ongoing initiatives and programs making a difference in communities worldwide
        </p>
        
        <!-- Search Bar -->
        <div class="max-w-md mx-auto relative">
          <div class="relative">
            <input 
              v-model="searchQuery" 
              type="text" 
              placeholder="Search activities..."
              class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition-all duration-200"
              @input="handleSearch"
            >
            <svg class="absolute right-3 top-3.5 h-5 w-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
            </svg>
          </div>
          
          <!-- Category Filter -->
          <div class="flex flex-wrap justify-center gap-2 mt-4">
            <button 
              v-for="category in categories" 
              :key="category.value" 
              @click="toggleCategory(category.value)"
              class="px-3 py-1 text-sm rounded-full transition-colors" 
              :class="getCategoryButtonClass(category.value)"
            >
              {{ category.label }}
            </button>
          </div>
        </div>
      </div>

      <!-- No Results Message -->
      <div v-if="filteredActivities.length === 0" class="text-center py-12">
        <svg class="mx-auto h-12 w-12 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
        </svg>
        <h3 class="mt-2 text-lg font-medium text-gray-900">No activities found</h3>
        <p class="mt-1 text-gray-500">Try adjusting your search or filter to find what you're looking for.</p>
        <button 
          @click="resetFilters"
          class="mt-4 px-4 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 transition-colors"
        >
          Reset filters
        </button>
      </div>

      <!-- Activities Grid -->
      <div v-else class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <article 
          v-for="(activity, index) in filteredActivities.slice(0, visibleItems)" 
          :key="index"
          class="group bg-white rounded-xl shadow-md overflow-hidden hover:shadow-lg transition-shadow duration-300 h-full flex flex-col"
        >
          <!-- Image Section -->
          <div class="h-48 overflow-hidden">
            <img 
              :src="activity.image" 
              :alt="activity.title"
              class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105"
            >
          </div>
          
          <div class="p-6 md:p-8 flex-grow">
            <!-- Category Badge and Date -->
            <div class="flex items-center justify-between mb-4">
              <span 
                class="inline-block px-3 py-1 text-xs font-semibold rounded-full"
                :class="getCategoryBadgeClass(activity.category)"
              >
                {{ getCategoryLabel(activity.category) }}
              </span>
              <span class="text-sm text-gray-500">{{ formatDate(activity.date) }}</span>
            </div>
            
            <!-- Title -->
            <h3 class="text-xl font-bold text-gray-900 mb-3 group-hover:text-blue-600 transition-colors">
              {{ activity.title }}
            </h3>
            
            <!-- Location -->
            <p v-if="activity.location" class="text-sm text-gray-500 mb-2">📍 {{ activity.location }}</p>
            
            <!-- Content Preview -->
            <p class="text-gray-600 mb-4 line-clamp-3">{{ activity.content }}</p>
            
            <!-- Author -->
            <div class="mt-auto">
              <span class="text-sm font-medium text-gray-500">By {{ activity.author }}</span>
            </div>
          </div>
          
          <!-- Learn More Button -->
          <div class="px-6 pb-6 md:px-8">
            <button
              class="w-full px-4 py-2 bg-blue-50 text-blue-600 rounded-md hover:bg-blue-100 transition-colors flex items-center justify-center"
              @click="viewActivityDetail(activity, index)"
            >
              Learn more
              <svg class="w-4 h-4 ml-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
              </svg>
            </button>
          </div>
        </article>
      </div>

      <!-- Load More Button -->
      <div v-if="filteredActivities.length > visibleItems" class="mt-12 text-center">
        <button 
          @click="loadMore"
          class="px-6 py-3 bg-white border border-gray-300 rounded-md text-gray-700 font-medium hover:bg-gray-50 transition-colors"
        >
          Load More Activities
        </button>
      </div>
    </div>

    <!-- Activity Detail View -->
    <div v-if="currentView === 'detail'" class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      <!-- Back Button -->
      <button 
        @click="backToListing"
        class="flex items-center space-x-2 text-gray-600 hover:text-gray-800 mb-6 transition-colors"
      >
        <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"/>
        </svg>
        <span>Back to Activities</span>
      </button>

      <article class="bg-white rounded-xl shadow-sm overflow-hidden">
        <!-- Hero Image -->
        <div class="aspect-video overflow-hidden">
          <img 
            :src="selectedActivity.image"
            :alt="selectedActivity.title"
            class="w-full h-full object-cover"
          >
        </div>
        
        <!-- Article Content -->
        <div class="p-8">
          <!-- Article Header -->
          <div class="mb-6">
            <div class="flex items-center justify-between mb-4">
              <span 
                class="px-3 py-1 text-sm font-medium rounded-full"
                :class="getCategoryBadgeClass(selectedActivity.category)"
              >
                {{ getCategoryLabel(selectedActivity.category) }}
              </span>
              <span class="text-sm text-gray-500">{{ formatDate(selectedActivity.date) }}</span>
            </div>
            
            <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-4">
              {{ selectedActivity.title }}
            </h1>
            
            <div class="flex items-center space-x-4 text-sm text-gray-500 mb-6">
              <span>By {{ selectedActivity.author }}</span>
              <span>•</span>
              <span>{{ calculateReadTime(selectedActivity.content) }} min read</span>
              <span v-if="selectedActivity.location">•</span>
              <span v-if="selectedActivity.location">📍 {{ selectedActivity.location }}</span>
            </div>
          </div>
          
          <!-- Article Body -->
          <div class="prose prose-lg max-w-none">
            <div class="text-gray-700 leading-relaxed whitespace-pre-line">{{ selectedActivity.content }}</div>
          </div>
          
          <!-- Call to Action -->
          <div class="mt-8 p-6 bg-pink-50 rounded-lg text-center">
            <h3 class="text-xl font-bold text-gray-900 mb-2">Support Our Mission</h3>
            <p class="text-gray-600 mb-4">
              Help us continue empowering communities through education, sports, and sustainable development.
            </p>
            <button class="bg-pink-600 text-white px-8 py-3 rounded-lg hover:bg-pink-700 transition-colors font-medium">
              Get Involved Today
            </button>
          </div>
        </div>
      </article>

      <!-- Related Activities -->
      <div v-if="relatedActivities.length > 0" class="mt-12">
        <h3 class="text-2xl font-bold text-gray-900 mb-6">Related Activities</h3>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <article 
            v-for="activity in relatedActivities"
            :key="activity.title"
            class="bg-white rounded-lg shadow-sm overflow-hidden hover:shadow-md transition-shadow cursor-pointer"
            @click="viewActivityDetail(activity)"
          >
            <div class="flex">
              <div class="w-24 h-24 flex-shrink-0">
                <img 
                  :src="activity.image"
                  :alt="activity.title"
                  class="w-full h-full object-cover"
                >
              </div>
              <div class="p-4 flex-1">
                <h4 class="font-semibold text-gray-900 mb-1 line-clamp-2">{{ activity.title }}</h4>
                <p class="text-sm text-gray-500">{{ activity.author }} • {{ formatDate(activity.date) }}</p>
              </div>
            </div>
          </article>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// View state management
const currentView = ref('listing') // 'listing' or 'detail'
const selectedActivity = ref(null)

// Reactive variables
const visibleItems = ref(6)
const searchQuery = ref('')
const activeCategories = ref([])

const categories = [
  { value: 'sports', label: 'Sports Programs' },
  { value: 'education', label: 'Education' },
  { value: 'community', label: 'Community Development' },
  { value: 'outreach', label: 'Outreach' }
]

const activities = [
  {
    title: "Girls Football Training Program - Jharkhand",
    content: "Our ongoing girls football training program in Jharkhand continues to empower young women through sports. This month, we conducted intensive training sessions for 150+ girls across 12 villages, focusing on skill development, teamwork, and leadership. The program includes weekly training sessions, monthly tournaments, and mentorship opportunities.\n\nParticipants have shown remarkable improvement in confidence, physical fitness, and academic performance. The program also provides nutritional support and educational workshops on health and hygiene. Local communities have embraced the initiative, with parents actively supporting their daughters' participation in sports activities.\n\nThe training sessions are conducted by certified coaches and include both technical skills and life skills development. We've seen a 40% increase in school attendance among participants and improved academic performance across the board.",
    date: "2024-12-15",
    author: "Sports Coordinator Team",
    category: "sports",
    image: "https://images.unsplash.com/photo-1540747913346-19e32dc3e97e?ixlib=rb-4.0.3&auto=format&fit=crop&w=1605&q=80",
    location: "Jharkhand, India"
  },
  {
    title: "Buddha Smiles Mobile Education Initiative",
    content: "Our Buddha Smiles mobile education program reached 8 remote villages this month, providing quality education to over 300 children. The program focuses on interactive learning through art, music, and storytelling. We've established temporary learning centers in community halls and conducted teacher training workshops for local educators.\n\nThe initiative includes digital literacy programs, creative arts workshops, and basic health education. Children have shown significant improvement in reading and numeracy skills. The program also engages parents through evening sessions on child development and educational support at home.\n\nThis month we introduced new learning modules focusing on environmental awareness and sustainable practices. The mobile units are equipped with solar panels, tablets, and interactive learning materials that make education engaging and accessible.",
    date: "2024-12-10",
    author: "Education Team",
    category: "education",
    image: "https://images.unsplash.com/photo-1523050854058-8df90110c9f1?ixlib=rb-4.0.3&auto=format&fit=crop&w=1470&q=80",
    location: "Tamil Nadu, India"
  },
  {
    title: "Community Water Well Installation Project",
    content: "Successfully completed the installation of 5 new water wells in remote tribal communities of Jharkhand. This project provides clean drinking water access to over 500 families. The installation process involved community participation, technical training for local maintenance, and establishment of water management committees.\n\nEach well is equipped with solar-powered pumps and water purification systems. The project also includes hygiene education programs and training for sustainable water resource management. Community members have been trained in basic maintenance and repair procedures to ensure long-term sustainability.\n\nThe impact has been immediate and significant - reducing water-borne diseases by 60% and freeing up time for children (especially girls) to attend school instead of walking long distances for water collection.",
    date: "2024-11-28",
    author: "Community Development Team",
    category: "community",
    image: "https://images.unsplash.com/photo-1464037866556-6812c9d1c72e?ixlib=rb-4.0.3&auto=format&fit=crop&w=1470&q=80",
    location: "Jharkhand, India"
  },
  {
    title: "CATALYST Scholarship Program Expansion",
    content: "Expanded our CATALYST scholarship program to support 50 additional university students from disadvantaged backgrounds. The program provides full tuition support, mentorship, and career guidance. This month's activities included orientation sessions, academic counseling, and skill development workshops.\n\nStudents participated in leadership training, community service projects, and internship placements. The program also includes mental health support and peer mentoring systems. Recipients have maintained an average GPA of 3.7 and 95% retention rate.\n\nMany scholars are now giving back to their communities through volunteer teaching and awareness programs. The expansion includes new partnerships with tech companies for internship opportunities and job placements upon graduation.",
    date: "2024-11-20",
    author: "Scholarship Program Team",
    category: "education",
    image: "https://images.unsplash.com/photo-1524179091875-bf99a9a6af57?ixlib=rb-4.0.3&auto=format&fit=crop&w=1470&q=80",
    location: "Cambodia"
  },
  {
    title: "Women's Empowerment Workshop Series",
    content: "Conducted a comprehensive women's empowerment workshop series across 15 villages, reaching over 400 women. The workshops covered financial literacy, entrepreneurship, health awareness, and legal rights. Participants learned about microfinance opportunities, business planning, and marketing strategies.\n\nThe program includes ongoing mentorship and access to small business loans. Several women have started their own enterprises, including tailoring, food processing, and handicraft businesses. The initiative also addresses gender equality issues and promotes women's participation in community decision-making processes.\n\nWe've established women's self-help groups in each village, creating sustainable support networks. The economic impact has been remarkable - participating women have increased their household income by an average of 45%.",
    date: "2024-11-15",
    author: "Women's Empowerment Team",
    category: "community",
    image: "https://images.unsplash.com/photo-1521791055366-0d553872125f?ixlib=rb-4.0.3&auto=format&fit=crop&w=1469&q=80",
    location: "Multiple locations, India"
  },
  {
    title: "Health Outreach Mobile Clinic Program",
    content: "Our mobile health clinic program provided medical services to 25 remote villages this quarter, serving over 1,200 patients. Services included general health checkups, vaccinations, maternal health care, and health education sessions. The program focuses on preventive care and early detection of common health issues.\n\nWe've established partnerships with local health workers and trained community health volunteers. The clinic also provides free medications and medical supplies. Special attention is given to women's health, child nutrition, and elderly care.\n\nThe program has significantly reduced travel time and costs for accessing healthcare in remote areas. We've seen a 50% reduction in preventable diseases and improved maternal and child health outcomes across all served communities.",
    date: "2024-11-08",
    author: "Health Outreach Team",
    category: "outreach",
    image: "https://images.unsplash.com/photo-1559757148-5c350d0d3c56?ixlib=rb-4.0.3&auto=format&fit=crop&w=1470&q=80",
    location: "Rural India"
  }
]

// Computed properties
const filteredActivities = computed(() => {
  const query = searchQuery.value.toLowerCase().trim()
  const hasSearchQuery = query !== ''
  const hasActiveCategories = activeCategories.value.length > 0

  return activities.filter(activity => {
    const matchesCategory = !hasActiveCategories || activeCategories.value.includes(activity.category)
    
    let matchesSearch = false
    if (hasSearchQuery) {
      const matchedCategory = categories.find(cat => 
        cat.label.toLowerCase().includes(query)
      )
      if (matchedCategory) {
        matchesSearch = activity.category === matchedCategory.value
      } else {
        matchesSearch = 
          activity.title.toLowerCase().includes(query) ||
          activity.content.toLowerCase().includes(query) ||
          activity.author.toLowerCase().includes(query) ||
          (activity.location && activity.location.toLowerCase().includes(query))
      }
    } else {
      matchesSearch = true
    }
    
    return matchesCategory && matchesSearch
  }).sort((a, b) => new Date(b.date) - new Date(a.date))
})

const relatedActivities = computed(() => {
  if (!selectedActivity.value) return []
  return activities.filter(activity => 
    activity.title !== selectedActivity.value.title &&
    (activity.category === selectedActivity.value.category || Math.random() > 0.5)
  ).slice(0, 2)
})

// Methods
const viewActivityDetail = (activity, index = null) => {
  selectedActivity.value = activity
  currentView.value = 'detail'
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const backToListing = () => {
  currentView.value = 'listing'
  selectedActivity.value = null
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const calculateReadTime = (content) => {
  const wordsPerMinute = 200
  const wordCount = content.split(/\s+/).length
  return Math.ceil(wordCount / wordsPerMinute)
}

const getCategoryButtonClass = (category) => {
  const isActive = activeCategories.value.includes(category)
  return {
    'bg-blue-100 text-blue-800': category === 'sports' && isActive,
    'bg-green-100 text-green-800': category === 'education' && isActive,
    'bg-purple-100 text-purple-800': category === 'community' && isActive,
    'bg-orange-100 text-orange-800': category === 'outreach' && isActive,
    'bg-gray-100 text-gray-800': !isActive
  }
}

const getCategoryBadgeClass = (category) => {
  return {
    'bg-blue-100 text-blue-800': category === 'sports',
    'bg-green-100 text-green-800': category === 'education',
    'bg-purple-100 text-purple-800': category === 'community',
    'bg-orange-100 text-orange-800': category === 'outreach'
  }
}

const loadMore = () => {
  visibleItems.value += 3
}

const handleSearch = () => {
  visibleItems.value = 6
}

const toggleCategory = (category) => {
  const index = activeCategories.value.indexOf(category)
  if (index === -1) {
    activeCategories.value.push(category)
  } else {
    activeCategories.value.splice(index, 1)
  }
  visibleItems.value = 6
}

const resetFilters = () => {
  searchQuery.value = ''
  activeCategories.value = []
  visibleItems.value = 6
}

const formatDate = (dateString) => {
  const options = { year: 'numeric', month: 'long', day: 'numeric' }
  return new Date(dateString).toLocaleDateString('en-US', options)
}

const getCategoryLabel = (category) => {
  const labels = {
    sports: 'Sports Programs',
    education: 'Education',
    community: 'Community Development',
    outreach: 'Outreach'
  }
  return labels[category] || 'Activity'
}
</script>

<style scoped>
/* Custom styles */
.line-clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.prose {
  line-height: 1.75;
}

.prose p {
  margin-bottom: 1.25em;
}

/* Image styles */
.h-48 {
  height: 12rem;
}

.h-64 {
  height: 16rem;
}

.object-cover {
  object-fit: cover;
}

.aspect-video {
  aspect-ratio: 16 / 9;
}

/* Transition effects */
.transition-all {
  transition-property: all;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 150ms;
}
</style>