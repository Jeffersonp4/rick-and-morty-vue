<template>
  <section>
    <div class="characters">
      <div
        class="character__item"
        v-for="character in characters"
        :key="character.id"
      >
        <CardCharacter :character="character" />
      </div>
    </div>
  </section>
</template>

<script>
import { computed, onMounted } from "vue";
import { useStore } from "vuex";

import CardCharacter from "./CardCharacter.vue";
export default {
  components: {
    CardCharacter,
  },
  setup() {
    const store = useStore();
    const characters = computed(() => {
      return store.state.charactersFilter;
    });

    // OnMounted es parte del ciclo de vida de los componentes en vue, dentro de este podemos llamar a las diferentes funciones de tu store
    onMounted(() => {
      // la extensin de store.dispatch te permite acceder a las actions de tu store
      store.dispatch("getCharacters");
    });

    return {
      characters,
    };
  },
};
</script>

<style>
.characters {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 3rem;
  margin: 3rem 0;
}
</style>
