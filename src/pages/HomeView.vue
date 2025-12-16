<script setup>
import axios from 'axios'

const episodes = ref([])
const page = ref(1)
const totalPages = ref(0)

const modalRef = ref(null)
const selectedEpisode = ref(null)
const characters = ref([])
const loadingCharacters = ref(false)

async function handleGetEpsodes() {
  try {
    const response = await axios.get('https://rickandmortyapi.com/api/episode', {
      params: {
        page: page.value,
      },
    })
    const episodesData = response.data.results
    totalPages.value = response.data.info.pages
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

async function openEpisodeDetails(episode) {
  selectedEpisode.value = episode
  characters.value = []
  loadingCharacters.value = true
  modalRef.value.open()

  try {
    // Busca todos os personagens do episódio
    const characterPromises = episode.characters.map((url) => axios.get(url))
    const characterResponses = await Promise.all(characterPromises)
    characters.value = characterResponses.map((res) => res.data)
  } catch (error) {
    console.error('Error fetching characters:', error)
  } finally {
    loadingCharacters.value = false
  }
}

function goToPage(p) {
  page.value = p
  handleGetEpsodes()
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
          class="cursor-pointer hover:shadow-lg transition-shadow"
          @click="openEpisodeDetails(episode)"
        />
      </div>
    </div>
    <PaginationBase
      :total-pages="totalPages"
      :current-page="page"
      @update:current-page="goToPage"
    />

    <!-- Modal de detalhes do episódio -->
    <ModalBase
      ref="modalRef"
      id="episode-modal"
      :title="selectedEpisode?.name"
    >
      <div v-if="selectedEpisode">
        <div class="mb-4">
          <p><strong>Episódio:</strong> {{ selectedEpisode.episode }}</p>
          <p><strong>Data de exibição:</strong> {{ selectedEpisode.air_date }}</p>
        </div>

        <h4 class="font-bold mb-2">Personagens ({{ characters.length }})</h4>

        <LoadingSpinner v-if="loadingCharacters" />

        <div v-else class="grid grid-cols-3 gap-2 max-h-64 overflow-y-auto">
          <AvatarItem
            v-for="character in characters"
            :key="character.id"
            :src="character.image"
            :name="character.name"
          />
        </div>
      </div>
    </ModalBase>
  </DefaultLayout>
</template>
