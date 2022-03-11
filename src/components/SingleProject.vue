<template>
  <div class="project" :class="{complete: project.complete }">
    <div class="actions">
      <h3 @click="handleDetails">{{ project.title }}</h3>
      <div class="icons">
          <router-link :to="{name : 'EditProject', params: {id: project.id}}"
          >
          <i  class="icon edit fa fa-pencil" aria-hidden="true"></i>
          </router-link>
        
        <i @click="deleteProject" class="icon trash fa fa-trash-o" aria-hidden="true"></i>
        <i @click="toggleComplete" class="icon check fa fa-check" aria-hidden="true"></i>

      </div>
    </div>
    <div v-if="showDetails" class="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      uri: "http://localhost:3000/projects/" + this.project.id
    };
  },
  methods: {
    handleDetails() {
      this.showDetails = !this.showDetails;
    },
    deleteProject() {
        fetch(this.uri, { method: "DELETE"})
        .then(() => this.$emit('delete', this.project.id))
        .catch(err => console.log(err.message))
    },
    toggleComplete() {
        fetch(this.uri, {
            method: "PATCH",
            headers: {"Content-Type": "application/json"},
            body: JSON.stringify({ complete: !this.project.complete })
            })
        .then(()=> {
            this.$emit('complete', this.project.id)
        })
        .catch(err => console.log(err.message))
        
    }
  },
};
</script>

<style>
.project {
  margin: 20px auto;
  background-color: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-left: 4px solid #e90074;
}

h3 {
  cursor: pointer;
}

.actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.icon {
    font-size: 24px;
    margin-left: 10px;
    
    cursor: pointer;
}

.edit {
    color: blue;
}
.trash {
    color: crimson;
}
.check {
    color: rgb(190, 190, 190);
}

.icon:hover{
    color: #777;
}

.project.complete {
    border-left: 4px solid #00ce89
}

.project.complete .check {
    color: #00ce89
}

</style>