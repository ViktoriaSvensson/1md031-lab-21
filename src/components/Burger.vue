

<template>

 <div class= "theburgers">
   <h4>{{ burger.name }}</h4>
   <img v-bind:src= "burger.url"  alt="Span" title="Another in-line element" style="width: 200px; height: 120px;" >
   <br><ul>
     <li>{{ burger.kCal }}</li>
     <li>{{ burger.contain }}</li>
     <li> Contains <span id= "allergier" > {{ burger.lactose }}  </span></li>
     <li>Contains <span id= "allergier">{{ burger.gluten }}</span></li>
   </ul>
 </div>
</template>

<script>
export default {
  name: 'Burger',
  props: {
    burger: Object
  }
}

</script>



<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.theburgers {
    background-color: black;
    color: white;
    border-radius: 10px;
    padding: 20px;
    font-size: 150%;
}

.wrapper {
     display: grid;
     grid-gap: 50px;
     grid-template-columns: 350px;

     color: #444;

 }


</style>
