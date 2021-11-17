<template>
  <div> 
    
          <h3 v-bind:key=burger.name> {{burger.name}}</h3>
          <img v-bind:src="burger.url" alt="Span" style="width: 20vw">
          <ul>
            <li v-if="burger.laktos"> EJ <span class="innehåll">laktosfri</span></li>
            <li v-else>Laktos<span class="innehåll">fri</span></li>
            <li v-if="burger.gluten"> EJ <span class="innehåll">glutenfri</span></li>
            <li v-else>Gluten<span class="innehåll">fri</span></li>

            <li v-bind:key=burger.kCal> {{burger.kCal }} kalorier</li>

          </ul>

          
         
          <div> 
          
            <button v-on:click="raiseAmount(key)">
              Add Burger
            </button>

            <button v-on:click ="lessAmount(key)">
              Remove Burger
            </button>

          </div>
          <p> Antal burgare {{amountOrdered}}</p>
         
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
  
  raiseAmount: function(){
    this.amountOrdered++;
    console.log (this.burger);

  },
  lessAmount: function(){
    this.amountOrdered--;
    console.log ( this.burger);
  },

  addBurger: function () {
  this.amountOrdered += 1;
  this.$emit('orderedBurger', { name:   this.burger.name, 
                                amount: this.amountOrdered 
                              }
  );
},
}
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>





</style>
