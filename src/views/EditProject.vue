<template>
  <h1>Edit Project</h1>
    <form @submit.prevent="handleSubmit">
      <label for="title">Title</label>
      <input type="text" v-model="title" required>
      <label for="details">Details</label>
      <textarea required v-model="details"></textarea>
      <button>Mettre à jour le projet</button>
  </form>
</template>

<script>
export default {
    props: ['id'],
    data(){
        return {
            title: '',
            details: '',
            uri: "http://localhost:3000/projects/" +this.id
        }
    },
    mounted() {
        fetch(this.uri)
        .then(response => response.json())
        .then(data => {
            this.title = data.title,
            this.details = data.details
        })
    },
    methods: {
        handleSubmit() {
            

            fetch(this.uri, {
                method: "PATCH",
                headers: {'Content-Type' : 'application/json'},
                body: JSON.stringify({title: this.title, details: this.details})
            })
            .then(() => {
                this.$router.push('/')
            })
            .catch(err => console.log(err.message))
        }
    }
}
</script>

<style>

</style>