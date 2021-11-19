<template>
  <div> 
    
          <h3 v-bind:key=burger.name>{{burger.name}}</h3>
          <img v-bind:src="burger.url"  style="width: 20vw">
          <ul>
            <li v-if="burger.laktos"> Innehåller <span class="allergen">laktos</span></li>
           
            <li v-if="burger.gluten"> Innehåller <span class="allergen">gluten</span></li>


            <li v-bind:key=burger.kCal> {{burger.kCal }} kalorier</li>

          </ul>

          <div> 
          
            <button v-on:click="addBurger">
              Lägg till burgare
            </button>

            <button v-on:click ="removeBurger">
             Ta bort burgare
            </button>

          </div>
          <p> Antal {{burger.name}}: {{amountOrdered}}</p>
         
  </div>
        
</template>

<script>


export default {
  name: 'Burger',
  props: {
    burger: Object
  },
  data: function () {
  return {
    amountOrdered: 0,
  }
  
},

methods: {
  
  addBurger: function(){
    this.amountOrdered++;
    this.$emit('orderedBurger', 
      {name: this.burger.name,
      amount: this.amountOrdered
      }
      );


  },
  removeBurger: function(){
    if(this.amountOrdered<=0 ){
    
      return;
    }
    this.amountOrdered--;
  
  },

  
}
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.allergen{
   font-weight: bold;
}



</style>
