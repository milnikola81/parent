<template>
  <div class="animal-list">
    <!-- <form @submit.prevent>
      <label>Type</label>
      <br>
      <input v-model="newAnimal.type" type="text" placeholder="species...">
      <br>
      <br>
      <label>Name</label>
      <br>
      <input v-model="newAnimal.name" type="text" placeholder="name...">
      <br>
      <br>
      <label>Birth date</label>
      <br>
      <input v-model="newAnimal.birthDate" type="date" placeholder="birth date...">
      <br>
      <br>
      <label>Choose sector</label>
      <br>
      <select v-model="newAnimal.sector" @change="onChange($event)">
        <option disabled="disabled">Choose one</option>
        <option v-for="(sector, index) in sectors" :key="index" :value="sector">{{sector}}</option>
      </select>
      <br>
      <br>
      <button @click="addAnimal" type="submit">Add animal</button>
    </form> -->

    <table>
      <tr>
        <th>Type</th>
        <th>Name</th>
        <th>Birth date</th>
        <th>Sector</th>
      </tr>
      <tr v-for="(animal, index) in filteredAnimals" :key="index">
        <td>{{animal.type}}</td>
        <td>{{animal.name}}</td>
        <td v-if="animal.birthDate">{{animal.birthDate}}</td>
        <td v-else>Unknown</td>
        <td>{{animal.sector}}</td>
        <button @click="removeAnimal(animal)">Remove</button>
        <button @click="moveToTop(animal)">Move to top</button>
      </tr>
    </table>

    <!-- <table>
      <tr>
        <th>Type</th>
      </tr>
      <tr v-for="(sector, index) in sectors" :key="index">
        <td>{{sector}}</td>
        <button @click="showAnimals(sector)">Show Animals</button>
      </tr>
    </table> -->

    <form @submit.prevent>
      <!-- <v-checkbox
          v-for="(sector, index) in sectors" :key="index"
          v-model="checked"
          v-bind:value="sector"
          :label="sector"
          @change="handleChange($event)">
        </v-checkbox> -->
      <div v-for="(sector, index) in sectors" :key="index">
        <label for="">{{sector}}</label>
        <input v-model="checked" type="checkbox" :name="sector" :value="sector" @change="handleChange($event)"><br>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "Zoo",
  data() {
    return {
      animals: [
        {
          type: "Elephant",
          name: "Elmer",
          birthDate: "12.12.2012.",
          sector: "North"
        },
        {
          type: "Monkey",
          name: "Momir",
          birthDate: "11.11.2011.",
          sector: "South"
        },
        {
          type: "Alligator",
          name: "Aladin",
          birthDate: "10.10.2010.",
          sector: "East"
        },
        {
          type: "Parrot",
          name: "Pera",
          sector: "West"
        },
                {
          type: "Elephant",
          name: "Elmer",
          birthDate: "12.12.2012.",
          sector: "North"
        },
        {
          type: "Monkey",
          name: "Momir",
          birthDate: "11.11.2011.",
          sector: "South"
        },
        {
          type: "Alligator",
          name: "Aladin",
          birthDate: "10.10.2010.",
          sector: "East"
        },
        {
          type: "Parrot",
          name: "Pera",
          sector: "West"
        }
      ],
      newAnimal: {},
      sectors: ["North", "South", "East", "West"],
      checked: [],
      filteredAnimals: []
    };
  },
  methods: {
    removeAnimal(animal) {
      this.animals.splice(this.animals.indexOf(animal), 1);
    },
    moveToTop(animal) {
      let index = this.animals.indexOf(animal);
      this.animals.splice(index, 1);
      this.animals.unshift(animal);
    },
    addAnimal() {
      this.animals.push(this.newAnimal);
      this.newAnimal = {};
    },
    showAnimals(sector) {
      let sectorAnimals = [];
      this.animals.forEach(animal => {
        if (animal.sector === sector) {
          sectorAnimals.push(animal.type);
        }
      });
      alert(sectorAnimals);
    },
    handleChange(event) {
        if(this.checked.length === 0) {
          this.filteredAnimals = this.animals
        }
        else {
          this.filteredAnimals = []
          for(var i=0; i < this.animals.length; i++) {
            for(var j=0; j < this.checked.length; j++) {
              if(this.animals[i].sector === this.checked[j]) {
                this.filteredAnimals.push(this.animals[i])
              }
            }
          }
        }
    }
  },
  computed: {
      // filteredProducts: function() {
      //     return this.products.filter((product) => {
      //         return product.title.toLowerCase().match(this.search)
      //     });
      // }
  },
  created() {
    this.filteredAnimals = this.animals
  }
};
</script>

<style scoped>
form {
  text-align: left;
  margin-top: 2rem;
}
td {
  border: 1px solid black;
}
</style>


