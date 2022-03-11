<template>
  <nav class="filter-nav">
      <button :class="{active: current === 'all' }"
      @click="updateFilter('all')" 
      >Tous les projets</button>
      <button :class="{active: current === 'completed' }"
      @click="updateFilter('completed')" 
      >Complétés</button>
      <button :class="{active: current === 'ongoing' }"
      @click="updateFilter('ongoing')" 
      >En cours</button>
  </nav>
</template>

<script>
export default {
    props: ['current'],
    methods: {
        updateFilter(by) {
            this.$emit('filterChange', by);
            this.active = !this.active;
        }
    },
    
}
</script>

<style>
.filter-nav {
    display: flex;
    justify-content: space-around;
}

.filter-nav button {
    background-color: none;
    /* border: 1px solid gray; */
    border: none;
    border-radius: 5px;
    padding: 10px;
    color: #bbb;
    outline: none;
    font-size: 14px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
}

.filter-nav button:hover {
    background-color: #00ce89;
    color: #fc1bb1;
}
.filter-nav button.active {
    background-color: #00ce89;
    color: #ffffff;
}

</style>