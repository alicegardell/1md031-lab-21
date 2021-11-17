<template>
  
  <div class="header">
        <h1> Välkommen till BurgerOnline</h1>
    </div>

    <main>

        <section class="helamenyn">

            <h2>Välj din burgare</h2>
            <p>Nedan ser du dina valmöjligheter (yes its kinda sad on the lowkey)</p>
            <div class="wrapper">
                <Burger class="box" v-for="burger in burgers"
                v-bind:burger="burger"
                v-bind:key="burger.name"
                v-on:orderedBurger="addToOrder($event)"/>

            </div>

        </section>


        <section class="kundinfo">
            <h2>Kundinformation</h2>
            <p>Här kan du lämna uppgifter om dig själv för att kunna göra en beställning</p>
            <h3>Utkörningsinformation</h3>
            <form>

                <p>
                    <label for="firstname">Ditt fullständiga namn</label><br>
                    <input type="text" id="firstname" v-model="helanamn" required="required" placeholder="För och efternamn">
                </p>

                <p>
                    <label for="email">Mailadress</label><br>
                    <input type="email" id="email" v-model="email" required="required" placeholder="E-mail address">
                </p>
                <p>
                    <label for="hus">Husnummer</label><br>
                    <input type="number" id="hus" v-model="husnummer" placeholder="Ange numret på din bostad">
                </p>


                <p>
                    <label for="payment">Betalningsalternativ</label><br>
                    <select id="payment" v-model="pm">
                        <option>Kort</option>
                        <option selected="selected">Swish</option>
                        <option>Klarna</option>
                        <option>Faktura</option>
                    </select>
                </p>
              
                <div>
                  <h3>Kön</h3>
                  <input type="radio" id="female" v-model="kvinna" value="kvinna">
                  <label for="female">Kvinna</label><br>
                  <input type="radio" id="male" v-model="man" value="man">
                  <label for="male">Man</label><br>
                  <input type="radio" id="ickebinär" v-model="ickebinär" value="ickebinär" >
                  <label for="ickebinär">Ickebinär</label><br>
                  <input type="radio" id="nogender" v-model="inget" value="nogender" checked="checked">
                  <label for="nogender">Vill inte dela med mig</label><br>
                </div>
                
                <div>
                    <h3>Slutför</h3>
                    <button v-on:click="markDone(key)" >
                        <img src="https://icon-library.com/images/sending-icon/sending-icon-11.jpg"
                            style="width: 2rem;">
                        Slutför
                    </button>
                    
                </div>
            </form>
        </section>
    </main>

    <footer>
        <hr> &copy; 2021 Alice Gardell Inc.
    </footer>
 

</template>

<script>
import menu from '../assets/menu.json'
import Burger from '../components/Burger.vue'
import io from 'socket.io-client'

const socket = io();

/*
function MenuItem(name, url, kCal, laktos, gluten) {
  this.name= name;
  this.url = url; 
  this.kCal = kCal;
  this.laktos = laktos; 
  this.gluten = gluten;
  return this;
}

let Vegodrömmen = new MenuItem("Vegodrömmen", "https://folkofolk.se/sites/default/files/2021-05/vegoburgare_0.jpg","300",  false, true)
let Ostdrömmen = new MenuItem("Ostdrömmen", "https://umarka.sk/wp-content/uploads/2019/09/portfolio_single_01-4.jpg", "500", false, false)
let BBQdrömmen = new MenuItem("BBQdrömmen",   "https://hips.hearstapps.com/del.h-cdn.co/assets/15/24/1434148038-burgers-06.jpg", "250" ,  false, true)

let BurgerArray = [Vegodrömmen, Ostdrömmen, BBQdrömmen]
*/



export default {
  name: 'Home',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: menu.menu
    }
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },

    markDone:function() {
      console.log( this.helanamn, this.email,this.husnummer,this.pm, this.inget, this.ickebinär, this.man, this.kvinna );
    },
    addToOrder: function (event) {
  this.orderedBurger[event.name] = event.amount;
  },


    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: event.clientX - 10 - offset.x,
                                           y: event.clientY - 10 - offset.y },
                                orderItems: ["Beans", "Curry"]
                              }
                 );
    }
  }
}

</script>

<style>
  #map {
    width: 400px;
    height: 400px;
    background-color: red;

  }
  body{
    font-family: Arial;
    
}

.header {
    
    background: url('https://metromidsayap-water.gov.ph/wp-content/uploads/2016/11/Header-Background.jpg');
    
    padding:3rem;
    margin-left: 2rem;
    margin-right: 2rem;
    text-align: center;
    
}

h1 {font-size: 6vh;}
h2 {font-size: 4vh;}
p {font-size: 2.5vh;}

section{
    margin-left: 2rem;
    margin-right: 2rem;
}

.wrapper{
    display: grid;
    grid-gap:10vw; 
    grid-template-columns: 15rem 15rem 15rem;
    align-content: center;
    
}
.helamenyn>.wrapper>div>img{ width: 20vw; height: 30vh;}

.div1{ grid-column: 1 / span 1;}
.div2{ grid-column: 2 / span 1;}
.div3{ grid-column: 3 / span 1;}


.helamenyn{
    overflow: hidden;
    background-color:rgb(125, 114, 173);
    color:white;
}


.helamenyn>div{float:left;}

.helamenyn{border-style: dotted; border-color: white; margin: 1.5rem; padding:1.5rem}

.helamenyn > div{padding: 1.5rem;}



.kundinfo{
    background-color:rgb(146, 205, 223);
    clear: left;
    border-style: dotted; border-color: black;
}

.kundinfo{margin: 1.5rem; padding:1.5rem}


button:hover {

 background-color: rgb(137, 168, 235);
 cursor: pointer;
 }

#firstname{
   width: 12rem; height: 2rem;
}
#email{
    width: 12rem; height: 2rem;
 }
 #hus{
    width: 12rem; height: 2rem;
 }
 #payment{
    width: 12rem; height: 2rem;
 }

.kön{margin-bottom: 0rem;}
</style>
