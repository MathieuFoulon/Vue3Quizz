<template>
  <nav class="main-nav">
      <router-link :to="{name : 'Home'}">Projets</router-link>
      <router-link :to="{name : 'AddProject'}">Ajouter un projet</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style>

.main-nav {
    text-align: center;
    margin: 40px auto;
}

.main-nav a{
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: #e90074;
    font-size: 18px;
}
.main-nav a:hover{
    
    color: #00ce89;
    
}

a.router-link-active{
    border-bottom: 2px solid #00ce89;
    padding-bottom: 4px;
}

</style>