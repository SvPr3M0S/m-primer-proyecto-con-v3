<script setup>
import {ref, computed} from 'vue'

const name = "Vue dinamico";

//metodo - methods


const counter = ref(0); //let para que se sobre escriba ref =reactiva resiva un dato
const arraysFavoritos = ref([]);
//const i = ref(0);

const increment = () => {
  //console.log('aumentar contador's)
  //counter.value = counter.value + 1; //counter.value++;  
  //console.log(counter)
  counter.value++;  
};

const Disminuir = () => {
  //console.log('aumentar contador')
  //   counter2.value = counter2.value - 1; 
  //console.log(counter)
  counter.value--;  
};
 
const Reset = () => {
  //console.log('aumentar contador')
  //   counter.value = 0 ; 
  //   counter2.value = 0 ;
  //console.log(counter)
  counter.value = 0 ; 
};

const Add = () => {
    
   arraysFavoritos.value.push(counter.value)
    //arrayNumero.value[i.value] = counter.value;
    //i.value=i.value+1; 
   };

const bloquearBtnAdd = computed(() =>{ // computed vamos estar viendo en movimiento si el numero que esta en el arrays ya existe
  const numSearch = arraysFavoritos.value.find(num => num === counter.value) //devolver el numero siempre en cuando exista
  console.log(numSearch); // muestre el resultado numsearch en console 
  //if (numSearch===0) return true; //para que no se pueda agregar 0 varias veses
  //return numSearch ? true : false; //para que el boton se desabilite un a vez que se agrege 
  return numSearch || numSearch ===0 
}); 
  

const ClassCounter = computed(()=>{
    if(counter.value===0){
  return 'zero'
    }
    if(counter.value > 0){
  return 'positivo'
    }
    if(counter.value <0){
  return 'negativo'
    }
})

//<h2 :class="counter > 0 ? 'positivo' : 'negativo' " > 
        //{{ counter }} 
      //</h2>

</script>

<template>
  <div class="container text-center mt-3">
    <h1> Hola {{ name.toUpperCase() }}</h1>
  <h2 :class=ClassCounter>{{ counter }} </h2> 

  <div btn-group>
    <button @click="increment" class="btn btn-success">Aumentar</button>
       <button @click="Disminuir" class="btn btn-danger">Disminuir</button>
       <button @click="Reset" class="btn btn-secondary">Reset</button>    
       <button @click="Add" :disabled="bloquearBtnAdd" class="btn btn-primary" >Agregar</button>
  </div>  
<ul class="list-group mt-4">
  <li 
  class="list-group-item"
    v-for="num in arraysFavoritos"
    :key="index">
    {{ num }} 
    
  </li>
</ul>
  </div>
  
</template>

<style>

h1 {
  color:red;
}

.negativo{
  color:red;
}
.positivo{
  color:green;
}
.zero {
  color:peru;
}

</style>