<template>
    <div>
        <header>
            My Trello
        </header>
        <main>
            <p class="info-line">All: 0 tasks</p>
            <list-add></list-add>
            <br>
            <br>
            <div class="list-index">
                <list v-for="(item, index) in lists"
                    :key="item.id"
                    :title="item.title"
                    :cards="item.cards"
                    :listIndex="index"
                ></list>
            </div>
        </main>
    </div>
</template>

<script>
import ListAdd from './ListAdd.vue'
import List from './List.vue'
import { mapState } from 'vuex'
export default {
    components: {
        ListAdd,
        List
    },
    computed: {
        ...mapState([
            'lists'
        ]),
    },
}
</script>