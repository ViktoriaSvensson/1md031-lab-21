

<template>

  <div class= "theburgers">
    <h4>{{ burger.name }}</h4>
    <img v-bind:src= "burger.url"  alt="Span" title="Another in-line element" style="width: 200px; height: 120px;" >
    <br><ul>
      <li>{{ burger.kCal }}kCal</li>
      <li>{{ burger.contain }}</li>
      <li v-if= "burger.lactose" id="lactose"> Contains <span> lactose </span></li>
      <li v-if= "burger.gluten" id="gluten" >Contains gluten</li>
      <br>Amount ordered {{ amountOrdered }}
    </ul>
    <button v-on:click="increaseOrder" type="+1" id="amountButton">
      +
    </button>
    <button v-on:click="decreaseOrder" type="-1" id="amountButton">
      -
    </button>
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
    increaseOrder: function (){
      this.amountOrdered +=1;
      this.$emit('orderedBurger', { name:   this.burger.name,
                                  amount: this.amountOrdered
      }
    );
    },
    decreaseOrder: function (){

      if (this.amountOrdered >0){
        this.amountOrdered -=1;
      }
      this.$emit('orderedBurger', { name:   this.burger.name,
                                  amount: this.amountOrdered
      }
    );
    },


},
}
</script>



<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.theburgers {
  background-color: black;
  color: white;
  border-radius: 10px;
  padding: 15px;
  padding-left: 40px;
  font-size: 150%;
  margin-left: 10px;
}

.wrapper {
  display: grid;
  grid-gap: 50px;
  grid-template-columns: 350px;
  color: #444;

}

#amountButton{
  width: 50px;
  height: 50px;
  margin-left: 15px;
}



</style>
