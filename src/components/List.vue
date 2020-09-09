<template>
  <!-- ★ここから追記 -->
  <div class="list">
    <div class="listheader">
      <p class="list-title">{{ title }}</p>
      <div class="list-counter">total: {{totalCardList}}</div>
      <div class="deletelist" @click="removeList">×</div>
    </div>


    <!-- LIstコンポーネント内部(Lits.vue)でcardをドラックアンドドロップさせたいのでgropにcardを付与する -->
    <draggable group="cards" :list="cards" @end="$emit('change')">
      <Card v-for="(item, index) in cards"
      :body="item.body"
      :key="item.id"
      :cardIndex = "index"
      :listIndex = "listIndex"
      >
    </Card>
    </draggable>
    <CardAdd :listIndex="listIndex"></CardAdd>
  </div>
  <!-- ★ここまで追記 -->
</template>


<script>
import draggable from 'vuedraggable'
import CardAdd from './CardAdd'
import Card from './Card'
// ★ここから追記
export default {
  components: {
    CardAdd,
    Card,
    draggable,
  },
  props: {
    title: {
      type: String,
      required: true
    },
    cards:{
      type: Array,
      required:true
    },
    listIndex: {
      type: Number,
      required: true
    }
  },
  methods: {
    removeList: function() {
      if(confirm('本当にこのリストを削除しますか？')){
        this.$store.dispatch('removelist', { listIndex: this.listIndex })
      }
    },
  },
  computed:{
    totalCardList:function(){
        return this.cards.length;
    }
  }
}
// ★ここまで追記
</script>