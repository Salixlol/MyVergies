<template>
  <div>
    <div class="block">
      <h3 class="is-size-3 is-family-handwritten" v-html="$i18n.t('createWallet.aPaperKey')"/>
      <p v-html="$i18n.t('createWallet.aPaperKeyDescription')"/>
    </div>

    <div class="columns is-multiline">
      <div
        class="column is-one-third"
        v-for="(word, i) in words"
        :key="i+word"
      >
        <div class="tags are-medium has-addons">
          <span class="tag is-success">{{ i+1 }}</span>
          <span class="tag is-family-code has-text-weight-semibold expand-word" v-html="word"/>
        </div>
      </div>
    </div>

    <div v-if="confirm" class="columns">
      <div class="column">
        <div class="tags are-medium">
          <span
            v-for="(word, i) in randomWords" :key="i+word" v-html="word"
            class="tag is-family-code has-text-weight-semibold is-clickable"
            @click="selectedPaperKey.push(word)"
          />
        </div>
      </div>
    </div>

    <b-field align="right">
      <b-button
        icon-left="edit"
        :label="$i18n.t('createWallet.confirmPaperKey')"
        type="is-primary"
        @click="$emit('next')"
      />
    </b-field>
  </div>
</template>

<script>
export default {
  name: 'PaperKey',
  data () {
    return {
      confirm: false,
      selectedPaperKey: [],
      paperKey: [
        'Flee',
        'Cave',
        'Use',
        'Suffer',
        'Cat',
        'Radio',
        'Heart',
        'Same',
        'Frog',
        'Disease',
        'Topple',
        'Inspire'
      ]
    }
  },

  computed: {
    words () {
      return this.confirm ? this.selectedPaperKey : this.paperKey
    },

    randomWords () {
      const words = this.paperKey.filter(word => {
        return !this.selectedPaperKey.includes(word)
      })

      return this.shuffleWords(words)
    }
  },

  methods: {
    shuffleWords (words) {
      for (let i = words.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [words[i], words[j]] = [words[j], words[i]]
      }

      return words
    }
  }
}
</script>

<style>
.expand-word {
  flex-grow: 1;
}
</style>
