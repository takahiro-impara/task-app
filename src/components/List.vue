<template>
  <div class="list">
    <div class="listheader">
      <p class="list-title">{{ title }}</p>
      <div class="deltelist" @click="removeList">x</div>
    </div>
    <card v-for="(item, index) in cards"
          :body="item.body"
          :key="item.id"
          :cardIndex="index"
          :listIndex="listIndex"
    ></card>
    <card-add :listIndex="listIndex"></card-add>
  </div>
</template>
<script>
import CardAdd from './CardAdd.vue'
import Card from './Card.vue'

export default {
  components: {
    CardAdd,
    Card
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
  methods: {
    removeList: function() {
      if(confirm('本当にこのリストを削除しますか？')){
        this.$store.dispatch('removeList', { listIndex: this.listIndex})
      }
    }
  }
}
</script>