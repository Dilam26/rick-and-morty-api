<template>
    <section>
        <div class="characters">
            <div class="characters__item" v-for="character in characters" :key="character.id" >
            <CardCharacter :character="character" />
            </div>
        </div>
    </section>
</template>
<script>
import { onMounted, computed } from 'vue'
import { useStore } from 'vuex'
import CardCharacter from './CardCharacter.vue'
export default {
  components: { CardCharacter },
    setup(props) {
        const store = useStore()
        const characters = computed(()=>{
            return store.state.charactersFilter
        })
        onMounted(() => {
            store.dispatch('getCharacters')
        })

        return {
            characters
        }
    }
}
</script>
<style>
    .characters {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 3rem;
        margin: 3rem 0;
    }

    @media (max-width: 768px) {
        .characters {
            grid-template-columns: repeat(2, 1fr);
        }
    }

    @media (max-width: 478px) {
        .characters {
            grid-template-columns: repeat(1, 1fr);
        }
    }
</style>