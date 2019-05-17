<template>
  <div class="animal-app">
      <h1>Add Animal</h1>
      
      <form @submit.prevent>
        Species:<br>
        <input v-model="newAnimal.species" type="text" name="species">
        <br><br>
        Name:<br>
        <input v-model="newAnimal.name" type="text" name="name"><br><br>
        Date of Birth:<br>
        <input v-model="newAnimal.dateOfBirth" type="date" name="date">
        <br><br>
         
        <div>Choose one sector</div>
        <select v-model="newAnimal.sector">
          <option disabled="disabled">Choose one sector</option>
          <option v-for='(sector, index) in sectors' :key='index' v-bind:value='sector.name'>
          {{sector.name}}</option>
        </select>
        <br><br>
        <button type="submit" @click="addAnimal()">Add Animal</button>
      </form> 
      <h1 @click="updateTitle">{{title}}</h1>
      
      <table>
        <tr>
            <th>Species</th>
            <th>Name</th>
            <th>dateOfBirth</th>
            <th>Sector</th>
        </tr>
        <tr v-for="(animal, index) in animals" :key="index"> 
            <td>{{ animal.species }}</td>
            <td>{{ animal.name }}</td>
            <td>{{!animal.dateOfBirth ? 'Unknown' : animal.dateOfBirth}}</td>
            <td>{{animal.sector.name }}</td>
            
            <span>
                <button @click="removeAnimal(animal)">x</button>
            </span>

            <span>
                <button @click="moveToTop(animal)">↑</button>
            </span>

        </tr>
      </table>

    <h1>Sectors</h1>
    <table>
      <tr v-for="(sector, index) in sectors" :key="index"> 
        <td>{{ sector.name }}</td>
          <span>
            <button @click="showAnimal(sector)">Show Animal</button>
          </span>
      </tr>
    </table>
  </div>
</template>

<script>

const sectors = [
              { name: "Predator" },
              { name: "Majmun" },
              { name: "Vodozemac" }
            ]
export default {
  name: 'AnimalList',
  props:{
    
    title:{
      type:String
    }
   
    
  },
  data(){
        return{
            animals:[
                {
                    species:'Tiger',
                    name:'Mile',
                    dateOfBirth:false,
                    sector:sectors[0]
                },
                {
                    species:'Snake',
                    name:'Natasa',
                    dateOfBirth:'30.7.1994',
                    sector:sectors[2]
                },
                {
                    species:'Monkey',
                    name:'Doris',
                    dateOfBirth:false,
                    sector:sectors[1]
                },
                {
                    species:'Lion',
                    name:'Rade',
                    dateOfBirth:'4.8.1987',
                    sector:sectors[0]
                },
                {
                    species:'Turtle',
                    name:'Zoka',
                    dateOfBirth:'1.3.1965',
                    sector:sectors[2]
                }
            ],
            newAnimal:{
                sector: {}
            },
            sectors:sectors,
            
      }
    },

    methods:{
        removeAnimal(animal){
           let position = this.animals.indexOf(animal);
           this.animals.splice(position,1);
        },

        moveToTop(animal){
            let position = this.animals.indexOf(animal);
            if (position > 0) {
                this.animals.splice(position, 1);
                this.animals.unshift(animal);
              }
           
        },

        addAnimal(){
            // console.log(this.newAnimal)
         this.animals.push(this.newAnimal);
         this.newAnimal  = {}
        
        },

        showAnimal(sector){
          //console.log(sector)
          //console.log(this.animals)
          let lisOfAnimalinSector = []
          this.animals.forEach(animal => {
              //console.log(animal.sector)
              if(sector.name == animal.sector.name){
                lisOfAnimalinSector.push(animal.name)
                //console.log(lisOfAnimalinSector)
              }
            })

            alert(lisOfAnimalinSector)
        },
        updateTitle(){
            this.$emit('changedText', 'Welcome to our ZOO')
        }

    }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 80%;
  margin:0 auto;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}

</style>
