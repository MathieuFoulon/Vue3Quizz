<template>
  <form @submit.prevent="handleSubmit">
      <label for="title">Nom du projet</label>
      <input type="text" v-model="title" required>
      <label for="details">Détails</label>
      <textarea required v-model="details"></textarea>
      <button>Ajouter le projet</button>
  </form>
</template>

<script>
export default {
    data() {
        return {
            title: '',
            details: ''
        }
    },
    methods: {
        handleSubmit() {
            let project = {
                title: this.title,
                details: this.details,
                complete: false
            }

            fetch('http://localhost:3000/projects', {
                method: "POST",
                headers: {'Content-Type' : 'application/json'},
                body: JSON.stringify(project)
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

form {
    background: white;
    padding: 20px;
    border-radius: 10px;
}

label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0;
}

input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
}

textarea {
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
}

form button {
    display: block;
    margin: 20px auto 0;
    background-color: #00ce89;
    color: white;
    padding: 10px;
    border: 0;
    font-size: 1.2em;
    text-shadow: 1px black;
    border-radius: 4px;
    cursor: pointer;
}

</style>