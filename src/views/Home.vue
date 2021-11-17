
<template>

  <header class= "rubrik">
    <img src="https://www.activecatering.se/wp-content/uploads/sites/131/2014/10/header-restaurang.png" id="rubrikbild">
    <h1 id= "rubriktext"> Välkommen till BurgerOnline </h1>
  </header>





  <main>
    <section class ="burgermenu">
      <h2>Choose your burger</h2>
      <br><br>
      This is where you choose your burgers

      <!--<nav> Menu items </nav>-->


      <div class="wrapper">

        <Burger v-for="burger in burgers"
        v-bind:burger="burger"
        v-bind:key="burger.name"/>
      </div>
      <div id="map" v-on:click="addOrder">
        click here
      </div>

    </section>


    <section class= "personalinfo" style= "clear:left;">
      <hr> <!--gör en horisontell linje-->
      <h2>Customesrs information</h2>
      This is where you provide neccessary information
      <h4>Delivery informaiton:</h4>

      <p><label for="firstlastname" >
        Full name
      </label>
      <br>
      <input type="text" id="firstlastname" name="fn" required="required" placeholder="First- and Last name">
    </p>

    <p><label for="email">
      E-mail
    </label>
    <br>
    <input type="email" id="email" name="em" required="required" placeholder="E-mail address">
  </p>

  <p><label for="street">Street</label><br>
    <input type="text" id="street" name="fn" required="required" placeholder="Street name"></p>

    <p><label for="house">House</label><br>
      <input type="number" id="street" name="fn" required="required" placeholder="House number"></p>

      <p><label for="recipient"> Payment options</label><br>
        <select id="recipient" name="rcp">
          <option selected="selected">DebitCard</option>
          <option>CreditCard</option>
          <option>Swish</option>
        </select></p>


        <p>Gender<br>
          <input checked="checked" type="radio" id="Gender" name="fn">
          <label for="Gender">Female</label><br>

          <input type="radio" id="Gender" name="fn">
          <label for="Gender">Male </label><br>

          <input type="radio" id="Gender" name="fn">
          <label for="Gender">Do not wish to provide </label></p>


        </section>

        <button v-on:click="addOrder" type="submit" id="myButton">
          <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTbRUPEUTPTXcTAOKr5GN3B-pI9DHw9bh3mrw&usqp=CAU" style="width: 15px;">
          Place my order!
        </button>



      </main>
      <hr> <!--gör en horisontell linje-->


      <footer>
        End notes
      </footer>

    </template>



    <script>
    import Burger from '../components/Burger.vue'
    import io from 'socket.io-client'
    import menu from '../assets/menu.json'





    /* function MenuItems(name, kCal, url, contain, gluten, lactose) {
    this.name = name; // The *this* keyword refers to the object itself
    this.kCal=kCal;
    this.url = url;
    this.contain=contain;
    this.gluten= Boolean(gluten);
    this.lactose=Boolean(lactose);
  }

  const menit = [
  new MenuItems ("Chicken", 2000, "https://res.cloudinary.com/hemkop/image/upload/c_fill,g_auto:custom_no_override,h_347,q_auto,w_618/v1/recipeImages/9854146805790", "chicken", false, false),
  new MenuItems ("Vegetarian", 1500, "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRT4Ow2wkRDTW6mb6LDwaVPJX4SmveSV9Q03g&usqp=CAU", "vegetarian", true, true),
  new MenuItems ("Bacon and beef", 2000, "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR9vAYgYztYeZZKgeQqe-of_i7Tc03H0eOELg&usqp=CAU", "beef", true, true)];

  console.log(menit)

  */


  const socket = io();

  export default {
    name: 'Home',
    components: {
      Burger,

    },
    data: function () {
      return {
        burgers: menu
      }
    },
    methods: {
      getOrderNumber: function () {
        return Math.floor(Math.random()*100000);
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
      },



    }
    </script>

    <style>
    #map {
      width: 300px;
      height: 300px;
      background-color: red;
    }

    @import 'https://fonts.googleapis.com/css?family=Pacifico|Dosis';
    body{
      font-family: "Courier New", monospace;
    }

    .burgermenu{
      /*color: #ff5500;*/
      background-color: black; color: white;
    }
    #allergier{
      /*text-transform: uppercase;*/
      font-weight: bold;
    }

    .rubrik{
      color: black;
      background-color: white;
      width: 1145px;

      margin: 10px;
      border: 5px outset #DEB887;
      padding: 10px;
      overflow: hidden;
    }

    #rubrikbild{
      opacity: 0.6;
      width: 100%;
      height: 300px;
    }

    #rubriktext {
      text-align: center;
      position: absolute;
      margin-top: -200px;
    }

    .burgers{
      background-color: black;
    }

    .wrapper {
      display: grid;
      grid-gap: 50px;
      grid-template-columns: 350px 350px 350px; /*ställer in stolek på boxaran*/
      color: grey;
      /*grid-column-gap: 40px;*/
    }

    .personalinfo{
      /*margin: 500px;*/
      /*margin: 100px 500px 50px 500px;*/
      margin: 10px;
      border: 5px outset #DEB887;
      padding: 10px;

    }
    .burgermenu{
      margin: 10px;
      border: 5px outset  #DEB887;
      padding: 10px;
    }

    button:hover {
      background-color: #DEB887;
    }

    </style>
