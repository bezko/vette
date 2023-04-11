<template>    
        
  <vueper-slides>
  <vueper-slide
    v-for="(starship, i) in starships"
    :key="i"
    :title="starship.name"
>
    <template #content>
      <div class="starship">
      <h2>{{ starship.name }}</h2>
      <ul>
        <li>Manufacturer: {{ starship.manufacturer }}</li>
        <li>Cost: {{ starship.cost_in_credits }}</li>
        <li>length: {{ starship.length }}</li>
        <li>Max Atmospheric Speed: {{ starship.max_atmosphering_speed }}</li>
        <li>Crew: {{ starship.crew }}</li>
        <li>Cargo Capacity: {{ starship.cargo_capacity }}</li>
        <li>Consumables: {{ starship.consumables }}</li>
        <li>Hyperdrive Rating: {{ starship.hyperdrive_rating }}</li>
        <li>MGLT: {{ starship.MGLT }}</li>
        <li>Class: {{ starship.starship_class }}</li>
        <li>Pilots: 
          <a v-for="(url,j) in starship.pilots" :key="j"  @click="show_pilot(url)">{{ find_name(url) }}</a>   
        </li>
      </ul>
    </div>
    </template>
  </vueper-slide>
</vueper-slides>

<widget-container-modal />


</template>

<script>
import { VueperSlides, VueperSlide } from 'vueperslides'
import 'vueperslides/dist/vueperslides.css'
import {container,openModal} from "jenesius-vue-modal";
import PilotModal from "./PilotModal.vue";

import SpaceTravel from "space-travel";
const axios = require("axios");



export default {

  components: { VueperSlides, VueperSlide,WidgetContainerModal: container},
  data() {

    return {
      starships:[],
      people:[],
    }
  },
  methods:{
    find_name(url)
    {
      for (let i in this.people)
      {
        const person  = this.people[i];
        if (person.url == url)
        {
          return person.name;
        }
      }
      return "NOT_FOUND"
    },
    show_pilot(url)
    {
      console.log("URL is " + url  );
      for (let i in this.people)
      {
        const person  = this.people[i];
        if (person.url == url)
        {
          openModal(PilotModal, {pilot: person});
          return person;
        }
      }
      return null;

  }},
   
  async created() 
  {   
   
    new SpaceTravel({ canvas: document.getElementById("space-travel") }).start();

    let people_url = "https://swapi.dev/api/people";
    let starships_url = "https://swapi.dev/api/starships";
   


    while (people_url != null)
    {
      let response =  await axios.get(people_url);
      this.people =  this.people.concat(response.data.results);
      if (response.data.next)
      {
        people_url =  response.data.next;
      }
      else
      {
        people_url = null;
      }
       
    }

    while (starships_url != null)
    {
      let response =  await axios.get(starships_url);
      this.starships =  this.starships.concat(response.data.results);
      if (response.data.next)
      {
        starships_url =  response.data.next;
      }
      else
      {
        starships_url = null;
      }
       
    }
   


  }
}
  

</script>

<style>
#space-travel
{
  width : 100%;
  height: 100%;
  left:0;
  top:0;
  z-index:-1;
  position:absolute;
}
h1
{
  color: white;
  font-size: 48px;
  font-family: Arial, Helvetica, sans-serif;
  margin:12px;
  padding:12px;
}

#app
{
  margin:60px;
  padding:60px;
  border-radius: 36px;
  border: 6px solid white;
}


.vueperslide
{
  color:white;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 12px;
}
.vueperslide .starship
{
  padding: 30px 120px;
}

.vueperslide h2
{
  font-size:24px;
  margin:24px 0;
}

.vueperslide li
{
  margin:6px 0;
  font-size: 14px;
}

.vueperslide a
{
  margin: 0 12px;
  color:yellow;
  cursor: pointer;
}
</style>