<template>
  <nav class="navbar navbar-expand-md navbar-light bg-light">
    <div class="container">
      <a class="navbar-brand" href="#">TaskList</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="/">Home</a>
            <a class="nav-link active" aria-current="page" href="/latihan"
              >Latihan</a
            >
          </li>
        </ul>
      </div>
      <button @click="showDropdown = !showDropdown">klick</button>
      <div v-if="showDropdown" class="dropdown">
        <!-- Isi dropdown di sini -->
        <ul v-for="(task, i) in resultQuery" :key="i" :task="task">
          <li>{{ task[i].tittle }}</li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      showDropdown: false,
    }
  },
  tasks: [
    {
      title: 'Task 1',
      description: 'ini deskripsi',
      isDone: false,
      category: 'task 2',
    },
    {
      title: 'Task 2',
      description: 'ini deskripsi 2',
      isDone: false,
      category: 'task 2',
    },
    {
      title: 'Task 3',
      description: ' ini deskripsi 3',
      isDone: false,
      category: 'task 3',
    },
  ],
  searchQuery: '',

  computed: {
    resultQuery() {
      if (this.searchQuery) {
        return this.tasks.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(' ')
            .every((v) => item.title.toLowerCase().includes(v))
        })
      } else {
        console.log(this.tasks)
        return this.tasks
      }
    },
  },
}
</script>

<style>
button {
  display: none;
}
ul.navbar-nav li.nav-item {
 display: flex;
 justify-content: space-between;
}
</style>
