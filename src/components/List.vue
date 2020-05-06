<template>
  <div class="list">
    <div class="listheader">
      <p class="list-title">{{ title }}</p>
      <p class="list-counter">total: {{ totalCardInList }}</p>
      <div class="deltelist" @click="removeList">x</div>
    </div>
    <draggable group="cards" :list="cards" @end="$emit('change')">
      <card v-for="(item, index) in cards"
            :body="item.body"
            :key="item.id"
            :cardIndex="index"
            :listIndex="listIndex"
      ></card>
      <card-add :listIndex="listIndex"></card-add>
    </draggable>

  </div>
</template>
<script>
import CardAdd from './CardAdd.vue'
import Card from './Card.vue'
import draggable from 'vuedraggable'


export default {
  components: {
    CardAdd,
    Card,
    draggable
  },
  props: {
    title: {
      type: String,
      required: true
    },
    listIndex: {
      type: Number,
      required: true
    },
    cards: {
      type: Array,
      required: true
    }
  },
  computed: {
    totalCardInList() {
      return this.cards.length
    }
  },
  methods: {
    removeList: function() {
      if(confirm('本当にこのリストを削除しますか？')){
        this.$store.dispatch('removeList', { listIndex: this.listIndex})
      }
    }
  }
}
</script>