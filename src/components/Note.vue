<template>
  <span>
    <sup class="note" @click="note_open = true">{{ note_number }}</sup>
    <div class="notification is-link is-note" v-if="note_open == true">
      <button class="delete" @click="note_open = false"></button>
      <p v-html="content"></p>
    </div>
  </span>
</template>

<script>

export default {
  name: 'note',
  data () {
    return {
      note_open: false
    }
  },
  props: {
    content: {
      default: "",
      type: String
    },
    note_number: {
      default: 1,
      type: Number
    }
  }
}
</script>

<style lang="sass">

@import "colors.sass"

.note
  color: $nkb-darkblue
  text-decoration: none
  cursor: pointer

</style>
