<template>
  <section
    id="pendidikan"
    class="py-20 bg-gradient-to-r from-blue-100 via-blue-50 to-green-100 min-h-screen font-sans"
  >
    <div class="container mx-auto px-6">
      <SectionTitle title="PENDIDIKAN" />
      <div class="relative">
        <div
          class="absolute hidden md:block h-full border-r-2 border-gray-300"
          style="left: 50%"
        ></div>
        <div
          v-for="(edu, index) in educationHistory"
          :key="edu.id"
          class="mb-8 w-full"
        >
          <div
            :class="[
              'flex flex-col md:flex-row justify-between items-center w-full',
              index % 2 === 0 ? 'md:flex-row' : 'md:flex-row-reverse'
            ]"
          >
            <div class="w-full md:w-1/2 md:pr-8 flex justify-end md:justify-end">
              <div
                class="bg-white rounded-xl shadow-lg p-6 hover:shadow-2xl transition duration-300 flex items-center gap-4 w-full max-w-md"
              >
                <img :src="edu.logo" class="w-16 h-16 object-contain" />
                <div
                  :class="index % 2 === 0 ? 'text-right' : 'text-left'"
                  class="w-full"
                >
                  <p class="text-sm font-semibold text-blue-600 mb-1">
                    {{ edu.period }}
                  </p>
                  <h3 class="text-2xl font-bold text-gray-800 mb-1">
                    {{ edu.institution }}
                  </h3>
                  <p class="text-gray-600">{{ edu.major }}</p>
                </div>
              </div>
            </div>
            <div class="hidden md:flex w-1/2 justify-start md:justify-start">
              <div class="w-4 h-4 bg-blue-600 rounded-full z-10"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import axios from 'axios'
import { ref, onMounted } from 'vue'
import SectionTitle from './SectionTitle.vue'

const educationHistory = ref([])

onMounted(async () => {
  try {
    const response = await axios.get('/api/education')
    educationHistory.value = response.data
  } catch (error) {
    console.error(error)
  }
})
</script>
