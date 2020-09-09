<template>
<div>
  <header>
    my Trello
  </header>
  <main>
    <p class="info-line">All: {{totalCardCount}}tasks</p>
          <div class="list-index">
          <draggable >
            <List v-for="(item, index) in lists"
              :key="item.id"
              :title="item.title"
              :cards = "item.cards"
              :listIndex="index"
               @change="movingCard"
        ></List>
        <ListAdd></ListAdd>
          </draggable>
      </div>
  </main>
</div>
</template>

<script>
import draggable from 'vuedraggable'
import ListAdd from './ListAdd'
// ★ここから追記
import List from './List'
import { mapState } from 'vuex'
// ★ここまで追記

export default {
  components: {
    ListAdd,
    // ★追記
    List,
    draggable
  },
  // ★追記
  computed: {
    ...mapState([
      'lists'
    ]),
    totalCardCount(){
      return this.$store.getters.totalCardCount
    }
  },
  methods: {
  movingCard: function() {
    this.$store.dispatch('updateList', { lists: this.lists })
  },
}
}
</script>