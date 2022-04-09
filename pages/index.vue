<template>
  <div class="py-4">
    <div class="container">
      <div
        class="
          title
          border-bottom
          d-flex
          align-items-center
          justify-content-between
          py-2
        "
      >
        <h5>Task</h5>
        <div>

          <select v-model="kategori">
            <option value="">Semua Task</option>
            <option value="1">Task 1</option>
            <option value="2">Task 2</option>
            <option value="3">Task 3</option>
          </select>

        </div>
        <button
            class="btn btn-outline-secondary py-1 px-3"
            @click="ss = !ss"
          >
          {{ ss ? "Show" : "Hide" }}
          </button>
        <div class="d-flex align-items-center">
          <input
            type="text"
            class="form-control"
            placeholder="Search"
            v-model="searchQuery"
          />
          <span class="me-2">View As</span>
          <button
            class="btn btn-outline-secondary py-1 px-3"
            @click="isGrid = !isGrid"
          >
            {{ isGrid ? "Grid" : "List" }}
          </button>
        </div>
      </div>


      <div class="list-task row">
        <CardItem
        
          v-for="(tasks, i) in resultQuery"
          :key="i"
          :task="tasks"
          :isGrid="isGrid"
          :ss="ss"
          
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
    <div></div>
  </div>
</template>
<script>
import CardItem from "@/components/Card/CardItem.vue";

export default {
  components: {
    CardItem,
  },
  data() {
    return {
      searchQuery: "",
      kategori: "",
      tasks: [
        {
          title: "Task 1",
          description: "ini deskripsi",
          isDone: false,
          ss: false,
          kategori: "Low",
        },
        {
          title: "Task 2",
          description: "ini deskripsi 2",
          isDone: false,
          ss: false,
          kategori: "Mid",
        },
        {
          title: "Task 3",
          description: " ini deskripsi 3",
          isDone: false,
          kategori: "Mid",
        },
        {
          title: "Task 4",
          description: " ini deskripsi 4",
          isDone: false,
          kategori: "High",
        },
      ],
      isCreating: false,
      isGrid: false,
      ss: false,
    };
  },
  methods: {
    doSomething() {
      alert("`Nothing to see here~");
    },
  },
  computed: {
    // resultQuery() {
    //   if (this.searchQuery) {
    //     return this.tasks.filter((item) => {
    //       return this.searchQuery
    //         .toLowerCase()
    //         .split(" ")
    //         .every((v) => item.title.toLowerCase().includes(v));
    //     });
    //   } else {
    //     console.log(this.tasks);
    //     return this.tasks;
    //   }
    // },
    resultQuery() {
      if (this.kategori) {
        return this.tasks.filter((item) => {
          return this.kategori
            .toLowerCase()
            .split(" ")
            .every((v) => item.title.toLowerCase().includes(v));
        });
      } else {
        console.log(this.tasks);
        return this.tasks;
      }
    },
  },
};
</script>
<style></style>
