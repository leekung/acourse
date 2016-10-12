<template>
  <div class="ui basic segment" :class="{loading}" style="padding: 0; margin: 0; min-height: 100%;">
    <router-view></router-view>
    <success-modal ref="successModal"></success-modal>
    <error-modal ref="errorModal"></error-modal>
  </div>
</template>

<style>
  @import url('https://fonts.googleapis.com/icon?family=Material+Icons');
  @import url('../node_modules/material-design-lite/material.min.css');

  .hidden {
    display: none;
  }

  .text-center {
    text-align: center;
  }

  p.description {
    text-align: left;
    white-space: pre-wrap;
    word-break: break-word;
  }
</style>

<script>
  import { Loader, Document } from './services'
  import SuccessModal from './components/success-modal'
  import ErrorModal from './components/error-modal'

  export default {
    components: {
      SuccessModal,
      ErrorModal
    },
    data () {
      return {
        loader: Loader.state
      }
    },
    computed: {
      loading () {
        return !!this.loader.value
      }
    },
    created () {
      Document.$successModal
        .subscribe(
          ({title, description}) => {
            this.$refs.successModal.show(title, description)
          }
        )
      Document.$errorModal
        .subscribe(
          ({title, description}) => {
            this.$refs.errorModal.show(title, description)
          }
        )
    }
  }
</script>
