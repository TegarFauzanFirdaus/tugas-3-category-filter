<template>
  <div class="py-4">
    <div class="container">
      <div class="title border-bottom d-flex align-items-center py-2">
        <h5>Tasks</h5>

        <div class="dropdownn">
          <span @click="showDropdown = !showDropdown">Tampilkan Dropdown</span>
          <div v-if="showDropdown" class="dropdown">
            <ul v-for="tugas in category" :key="tugas.slug" mt-9>
              <li @click="tombolQuery(tugas.slug)">{{ tugas.nama }}</li>
            </ul>
          </div>
        </div>

        <div class="d-flex align-items-center ms-auto" style="width: 60%">
          <!-- /* Form input pencarian */ -->

          <input
            type="text"
            class="form-control"
            placeholder="Search"
            v-model="searchQuery"
          />

          <div class="event-grid d-flex align-items-center justify-content-end w-100">
            <span class="view-as me-2">View As</span>
            <button
              class="tombol btn btn-outline-secondary py-1 px-3"
              @click="isGrid = !isGrid"
            >
              {{ isGrid ? 'Grid' : 'List' }}
            </button>
          </div>
        </div>
      </div>

      <div class="list-task row">
        <CardItem
          v-for="(task, i) in resultQuery"
          :key="i"
          :task="task"
          :isGrid="isGrid"
        />
      </div>
      <div class="action py-2">
        <a
          href="#"
          class="add-button"
          v-if="!isCreating"
          @click="isCreating = !isCreating"
          >Add Task</a
        >
        <div class="add-card" v-else>
          <div class="card mb-2">
            <div class="card-body d-flex flex-column p-0">
              <input
                class="form-control border-0 mb-2"
                placeholder="Title"
                type="text"
              />
              <textarea
                class="form-control border-0 small"
                placeholder="Description"
                rows="3"
              ></textarea>
            </div>
          </div>
          <div class="button-wrapper d-flex">
            <button class="btn btn-primary me-2">Save</button>
            <button
              class="btn btn-outline-secondary"
              @click="isCreating = !isCreating"
            >
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CardItem from '@/components/Card/CardItem.vue'
export default {
  components: {
    CardItem,
  },
  layout(context) {
    return 'custom'
  },
  data() {
    return {
      showDropdown: false,

      // Tipe layout daftar task
      isGrid: false,
      // Status saat menambahkan task
      isCreating: false,
      isOpen: false,
      // Daftar task
      tasks: [
        {
          title: 'Task 1',
          description: 'ini deskripsi',
          isDone: false,
          category: 'unfinished',
        },
        {
          title: 'Task 2',
          description: 'ini deskripsi 2',
          isDone: false,
          category: 'unfinished',
        },
        {
          title: 'Task 3',
          description: ' ini deskripsi 3',
          isDone: false,
          category: 'finish',
        },
        {
          title: 'Task 4',
          description: ' ini deskripsi 4',
          isDone: false,
          category: 'finish',
        },
        {
          title: 'Task 5',
          description: ' ini deskripsi 5',
          isDone: false,
          category: 'finish',
        },
        {
          title: 'Task 6',
          description: ' ini deskripsi 6',
          isDone: false,
          category: 'unfinished',
        },
      ],
      category: [
        {
          nama: 'unfinished',
          slug: 'unfinished',
        },
        {
          nama: 'finish',
          slug: 'finish',
        },
      ],
      // Variabel penampung teks pencarian
      searchQuery: '',

      // Variabel penampung klik
      selectedCategory: '',
      // Status saat menambahkan task
      isCreating: false,
      // Tipe layout daftar task
      isGrid: false,
    }
  },

  methods: {
    tombolQuery(hasilklik) {
      this.selectedCategory = hasilklik
    },
    },
    toggleDropdown() {
      this.showDropdown = !this.showDropdown
    },
  computed: {
    resultQuery() {
      if (this.searchQuery) {
        return this.tasks.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(' ')
            .every((v) => item.title.toLowerCase().includes(v))
        })
      } else if (this.selectedCategory) { 
        return this.tasks.filter(item => item.category == (this.selectedCategory))
      }else {
        console.log(this.tasks)
        return this.tasks
      }
    },
  },
}
</script>

<style scoped>
.dropdownn {
  margin-left: 15%;
}
.dropdown {
  position: absolute;
  z-index: 10;
  right: 58.5%;
  background-color:rgb(21, 66, 21);
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-right: 1.5%;
  border-bottom-left-radius: 10px;
  border-bottom-right-radius: 10px;
}

ul li {
  position: relative;
  margin-top: 20%;
  display: inline-block;
  color: aliceblue;
}
div.title h5 {
  color: aliceblue;
}
div.dropdownn span {
color: aliceblue;
}
div.event-grid .view-as {
color: aliceblue;
}
div.event-grid .tombol {
    color: aliceblue;

}

.action a {
  text-decoration: none;
  color:rgb(0, 0, 0);
  font-size: 150%;
}


.action a:hover {
  color: rgb(19, 208, 19);
}

</style>
