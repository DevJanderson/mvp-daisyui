<script setup>
import axios from 'axios'

const episodes = ref([])

async function handleGetEpsodes() {
  try {
    const response = await axios.get('https://rickandmortyapi.com/api/episode')
    const episodesData = response.data.results

    // Busca os primeiros 4 personagens de cada episódio
    for (const episode of episodesData) {
      const characterUrls = episode.characters.slice(0, 4)
      const characterPromises = characterUrls.map((url) => axios.get(url))
      const characterResponses = await Promise.all(characterPromises)
      episode.avatars = characterResponses.map((res) => res.data.image)
    }

    episodes.value = episodesData
  } catch (error) {
    console.error('Error fetching episodes:', error)
  }
}

onMounted(() => {
  handleGetEpsodes()
})
</script>

<template>
  <DefaultLayout>
    <div class="container mx-auto p-4">
      <div class="flex flex-wrap gap-4 justify-center">
        <CardBase
          v-for="episode in episodes"
          :key="episode.id"
          :title="episode.name"
          :description="episode.air_date"
          :badge="episode.episode"
          :avatars="episode.avatars"
          :tags="[`${episode.characters.length} personagens`]"
        />
      </div>
    </div>
  </DefaultLayout>
</template>
