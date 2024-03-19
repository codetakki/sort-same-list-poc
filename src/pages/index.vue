<template>
  <div class="row">
    <h1>Demo of basic feature</h1>
    <h3>both Tables have the same array, and are draggable <br>
      you can move move a item from one list to the other and the item will update its position to the new index </h3>
      {{ lists[0].length }} - {{ lists[1].length }}
    <v-row>
      <v-col v-for="i in 2" :key="i">

        <v-table class="table table-striped" id="table">
          <thead class="thead-dark">
            <tr>
              <th scope="col">Id</th>
              <th scope="col">Name</th>
              <th scope="col">Sport</th>
            </tr>
          </thead>
          <draggable
            v-model="list"
            animation="50"
            selected-class="selected"
            @change="handelChange($event)"
            tag="tbody"
            item-key="id"
            
            :group="{ name: 'people', pull: true }"
          >
            <template #item="{ element, index }">
              <tr>
                <td scope="row">{{ element.id }}</td>
                <td>{{ element.name }}</td>
                <td>{{ element.sport }}</td>
              </tr>
            </template>
          </draggable>
        </v-table>

      </v-col>
      <!-- <v-col>
        <v-table class="table table-striped">
          <thead class="thead-dark">
            <tr>
              <th scope="col">Id</th>
              <th scope="col">Name</th>
              <th scope="col">Sport</th>
            </tr>
          </thead>
          <draggable
            v-model="list"
            tag="tbody"
            item-key="id"
            @change="handelChange($event)"
            :group="{ name: 'people', pull: true }"
          >
            <template #item="{ element }">
              <tr>
                <td scope="row">{{ element.id }}</td>
                <td>{{ element.name }}</td>
                <td>{{ element.sport }}</td>
              </tr>
            </template>
          </draggable>
        </v-table>
      </v-col> -->
    </v-row>

  </div>
</template>

<script>
import draggable from "vuedraggable";
export default {
  name: "table-example",
  display: "Table",
  order: 8,
  components: {
    draggable
  },
  data() {
    return {
      oneChange: false,
      lists: [
        [],
        []
      ],
      list: [
        { id: 1, name: "Abby", sport: "basket" },
        { id: 2, name: "Brooke", sport: "foot" },
        { id: 3, name: "Courtenay", sport: "volley" },
        { id: 4, name: "David", sport: "rugby" },
        { id: 5, name: "Emma", sport: "tennis" },
        { id: 6, name: "Finn", sport: "soccer" },
        { id: 7, name: "Grace", sport: "swimming" },
        { id: 8, name: "Henry", sport: "baseball" },
        { id: 9, name: "Isaac", sport: "hockey" },
        { id: 10, name: "Jasmine", sport: "badminton" },
        { id: 11, name: "Kai", sport: "cricket" },
        { id: 12, name: "Liam", sport: "golf" },
        { id: 13, name: "Mia", sport: "surfing" },
        { id: 14, name: "Noah", sport: "skiing" },
        { id: 15, name: "Olivia", sport: "snowboarding" },
        { id: 16, name: "Peyton", sport: "cycling" },
        { id: 17, name: "Quinn", sport: "running" },
        { id: 18, name: "Ryan", sport: "wrestling" },
        { id: 19, name: "Sophia", sport: "boxing" },
        { id: 20, name: "Tyler", sport: "surfing" }
      ],
      list2: [],
      dragging: false,
      lastindex: null
    };
  },
  watch: {
    list(value) {
      //console.log(value);
    }
  },
  mounted() {
    this.lists[0] = this.list
    this.lists[1] = this.list

  },
  methods: {
    clone(event){
      console.log("clone",event);
      this.list.splice(event.oldIndex, 1);
    },
    handelMove(event){
      console.log("move",event);
    },
    logChange(event){
      console.log(event);
    },
    handelChange(event) {
      console.log(event);
      if (event.added) {
        if(Array.isArray(event.added)){
          this.lastindex =  event.added.map(i=>i.newIndex)
        }
        else{
          this.lastindex = event.added.newIndex
        }
      }
      console.log(this.lastindex);
      if (event.removed) {
        if(Array.isArray(event.removed)){
          for (let index = 0; index < event.removed.length; index++) {
            const element = event.removed[index];
            console.log(element);
            this.list.splice(this.lastindex[index], 0,element.element);
          }
        }
        else{
          this.list.splice(this.lastindex, 0, event.removed.element);
        }
      }

    }
  }
};
</script>
<style scoped>
.buttons {
  margin-top: 35px;
}
.selected {
  color: red !important;
  background-color: rgba(255, 0, 0, 0.2) !important;
}
</style>
