<script setup>
import { ref } from "vue";

  const nom = ref("")
  const email = ref("")
  const tel = ref("")
  const message = ref('')
  const formHasErrors =ref(false)

  function validation(){
    formHasErrors.value = false
    try {
      if(!nom.value || !email.value || !tel.value){
        formHasErrors.value = true
        message.value = "Veuillez remplir les champs correctement "
        throw new Error("L'un de champs n'est pas rempli correctement.")
        
      }
      message.value = "Le formulaire est soumis avec succès."

    }catch(e){
      console.log(e.message)
      const messageErreur = e.message
      return messageErreur
    }
    
  }
</script>

<template>
  <form action="" @submit.prevent="validation">
    <label for="nom">Nom</label>
    <input type="text" name="nom" id="nom" v-model="nom">
    <label for="email">Email :</label>
    <input type="email" name="email" id="email" v-model="email">
    <label for="tel">Telephone : </label>
    <input type="tel" name="tel" id="tel" v-model="tel">
    <button>Soumettre</button>

  </form>
    <div>
      <h2>Message d'affichage</h2>
      <p> Nom : {{nom}}</p>
        <p>Email : {{email}}</p>
       <p> Telephone : {{tel}} </p>
       <p v-if="message" class="msg" :class="formHasErrors ? 'error' : 'success'">
        {{message}}
       </p>
    </div>
</template>

<style scoped>
  .error{
    color: red;
  }
  .success {
    color: green;
  }
</style>
