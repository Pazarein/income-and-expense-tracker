<template>
  <div class="income-list">
    <transition-group name="list" tag="p">
        <income-item-vue 
            v-for="data in state.sortedIncome" 
            :key="data.id" 
            :income="data" 
            @remove="remove" 
        />
    </transition-group>
        
  </div>
</template>

<script>
import IncomeItemVue from './IncomeItem.vue';

export default {
    components: {
        IncomeItemVue,
    },
    props: {
        state : Object
    },
    setup (props, { emit }) {
        function remove(id) {
            emit( 'remove', id );
        }
        return {
            remove
        }
    }
}
</script>

<style scoped>
.income-list{
    margin: 30px;
}
.list-item{
    margin-top: 30px;
    padding:15px;
}
.list-enter-active,
.list-leave-active {
  transition: all 0.4s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}

.list-move {
  transition: transform 0.4s ease;
}
</style>