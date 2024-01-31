<script setup lang="ts">
  import {ref} from 'vue'
  import type {Ref} from 'vue'

  const name:Ref<string> = ref('')
  const last_name:Ref<string> = ref('')
  const age:Ref<number> = ref(0)
  const gender = ref('')
  const other_gender:Ref<string> = ref('')


  const errors = ref ({
      name: '',
      last_name:'',
      age:'',
    });

  const validation = () => {
  if (name.value.length > 18 || name.value.length < 5){
    errors.value.name = 'El nombre debe tener entre 5 y 18 caracteres.'
  }else{
    errors.value.name = ''
  }

  if (last_name.value === name.value){
    errors.value.last_name = 'El apellido no debe ser igual al nombre'
  }else{
    errors.value.last_name = ''
  }

  if (age.value <  0){
    errors.value.age = 'La edad debe ser mayor a 0'
  }else if(age.value >= 60){
    errors.value.age = 'La edad debe ser menor a 60'
  }else{
    errors.value.age = ' '
  }
}
</script>

<template>
  <main> 
    <div :class="{'formulario':true}" @input="validation()">
      <input v-model="name" type="text">
      <p v-if="errors.name">{{ errors.name }}</p>
      <input v-model="last_name" type="text">
      <p v-if="errors.last_name">{{ errors.last_name }}</p>
      <input  v-model="age" type="number">
      <p v-if="errors.age">{{ errors.age }}</p>

      <div :class="{'select_form':true}">
        <input type="radio" id="masculino" value="Masculino" v-model="gender">
        <label for="masculino">Masculino</label>
        <input type="radio" id="femenino" value="Femenino" v-model="gender">
        <label for="femenino">Femenino</label>
        <input type="radio" id="otro" value="Otro" v-model="gender">
        <label for="otro">Otro</label>
      </div>

      <div v-if="gender.includes('Otro')" :class="{'genero':true}">
        <input v-model="other_gender" type="text">
      </div>

    </div>
  </main>
</template>

<style scoped>

.formulario{
  display: flex;
  border-radius: 15px;
  flex-direction: column;
  width: 70%;
  align-items: center;
  padding-top: 2rem;
  padding-bottom: 2rem;
  background-color: rgba(174, 134, 211, 0.671);
}

.formulario input{
  height: 2rem;
  width: 70%;
  padding-left: 10px;
  border-color: rgb(136, 27, 127);
  border-radius: 15px;
  margin-top: 2rem;
}

.formulario p{
  font-size: 18px;
  color: red;
}

.select_form input{
  height: 1rem;
  width: 2rem;
}
.select_form label{
font-size: 20px;
height: 2rem;
color: aliceblue;
margin-right: 2rem;
}

.invalido{
  border-color: red;
}
</style>