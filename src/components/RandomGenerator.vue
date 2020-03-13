<template>
  <div id='inputs'>
    <input id="min" placeholder="Minimum Value" v-model.number="min"/>
    <input id="max" placeholder="Maximum Value" v-model.number="max"/>
    <input id="count" placeholder="Count" v-model.number="count"/>
    <button id="btn" @click='generate({count, min, max})'>Generate</button>
    <p id='error_message'>{{error_message}} </p>
    <img id='cup1' src='cup.png' width=300 height=400 />
    <ul id="results">
      <li v-for="(num, index) in results">{{results[index]}} </li> 
    </ul>
    
    <img id='cup2' src='cup.png' width=300 height=400 />
  </div>
</template>
<style>
body{
  background-color: #f47920;
}
#cup1{
  grid-column: 2;
  grid-row: 3;
}
#cup2{
  grid-column: 4;
  grid-row: 3;
}
#results{
  padding-top: 5%;
  grid-column: 3;
  grid-row: 3;
}
#inputs li{
  font-size: 2em;
  list-style-type: none;
}
input{
    text-align: center;
    grid-row: 1;
}
#min{
  grid-column: 2;
}
#max{
  grid-column: 3;
}
#count{
  grid-column: 4;
}
#inputs{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
  grid-column-gap: 5%;
  padding-top: 3%;

}
#btn{
  grid-column: 3;
  grid-row: 2;
  margin-top: 10%;
  border: none;
  height: 75%;
}
#inputs input, #inputs button{
border-radius: 65px;
border: none;
 background-color: #FAA21B;
}

#inputs ul{
  margin-top: 20%;
  grid-column: 3;
}
#error_message{
  grid-column: 3;
  grid-row: 3;
}
</style>
<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  data() {
    return {
      results: new Array<number>(),
      count: '',
      min: '',
      max: '',
      error_message: ''

    };
  },
  methods: {
    generate({ count = 1, min = 1, max = 10 } = { count: 1, min: 1, max: 10 }): void {
      while(this.results.length > 0) {this.results.pop();}
      this.error_message = ''
      try {
        if (count==='' || min==='' || max==='') {
          throw new TypeError('At Least One Value is Empty');
        }
        else if (count < 1 || count > 10) {
          throw new TypeError("Count Must be Between 0 and 10");
        } 
        else if (min < 1 || min > max) {
            throw new Error('Minimum Value Must be Larger Than 0 and Less Than or Equal to Maximum Value');
          }
        else if (max < 1 || max < min) {
            throw new Error('Maximum Value Must be Larger Than 0 and Larger or Equal to Minimum Value');
          }
        else if (isNaN(count) || isNaN(min) || isNaN(max)){
          throw new Error('All Inputs Must be Numbers') 
        }
        else {
              for(let i = 0; i < count; i++) {
                const num = Math.floor(Math.random() * (max - min + 1) ) + min;
                this.results.push(num);
            }
        }
      } 
      catch(err) {
          // window.alert(err.message);
          this.error_message = 'Error: ' + err.message;
      }

    },
  },
});
</script>

<style scoped>

</style>