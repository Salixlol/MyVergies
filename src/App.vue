<template>
  <div id="app" class="app-container is-unselectable">
    <NavBar>
      <template slot="navbar-items">
        <div class="buttons">
          <a class="button is-white is-not-draggable">
            <b-icon icon="wifi" type="is-success" size="is-small"/>
          </a>
          <a class="button is-white is-not-draggable" @click="unlock">
              <span class="icon has-text-grey-dark">
                <b-icon size="is-small" icon="lock-open" />
              </span>
          </a>
          <router-link to="/settings" class="button is-white is-not-draggable">
              <span class="icon has-text-grey-dark">
                <b-icon size="is-small" icon="cog" />
              </span>
          </router-link>
          <router-link to="/help" class="button is-white is-not-draggable">
              <span class="icon has-text-grey-dark">
                <b-icon size="is-small" icon="question-circle" />
              </span>
          </router-link>
        </div>
      </template>
    </NavBar>
    <div class="columns is-gapless app-content-container is-marginless">
      <MainMenu class="column is-one-quarter" :wallets="wallets"/>
      <ContentContainer>
        <RouterView class="app-content-box-container"/>
      </ContentContainer>
    </div>
  </div>
</template>

<script>
import NavBar from '@/components/layout/NavBar'
import MainMenu from '@/components/layout/MainMenu'
import ContentContainer from '@/components/layout/ContentContainer'
import AuthenticationModal from '@/components/modals/AuthenticationModal'
import Wallets from '@/assets/data/example/wallets'

export default {
  name: 'my-vergies',
  components: { ContentContainer, MainMenu, NavBar },
  data () {
    return {
      wallets: Wallets
    }
  },
  methods: {
    unlock () {
      this.$buefy.modal.open({
        parent: this,
        component: AuthenticationModal,
        hasModalCard: true,
        canCancel: ['escape', 'outside'],
        fullScreen: true
      })
    }
  }
}
</script>

<style lang="scss">
  @import '~@/assets/scss/main';

  .app-container {
    height: 100%;
    background: #ebebeb;
    cursor: default;
  }

  .app-content-container {
    height: calc(100% - 52px);
  }

  .app-content-box-container {
    max-width: 1024px;
    margin: auto;
  }

  @media (prefers-color-scheme: dark) {
    .app-container {
      color: white;
      background: #1f2123;
    }
  }
</style>
