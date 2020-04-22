// App.vue 
<template>
  <div id="background">
    <div id="box">
      <h3>Add dialog.</h3>
      <input v-model="currentCharacter">
      <input v-model="newDialog" @keyup.enter="addDialog()">
      <button @click="addDialog()">Add</button>
      <br>
      <ul>
        <li v-for="item in dialogs">
          <!-- <span>{{item['name']}}</span> -->
          <img :src="item.imgURL" height="40">
          <span>{{item.dialog}}</span>
        </li>
      </ul>
      <hr>
      <h3>The characters in characters.json</h3>
      <ul>
        <li v-for="character in characters">
          <img :src="character.imgURL" height="40">
          {{character.name}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import data from "./characters.json";
let characters = data.characters;
export default Vue.extend({
  data() {
    return {
      counter: 0,
      newDialog: "Yo",
      currentCharacter: characters[0]['name'],
      dialogs: [
        { name: characters[0]['name'], dialog: "Can I get a witness?", imgURL: characters[0]['imgURL'] }
      ],
      newImage: "",
      img: "",
      characters: characters,
      images: []
    };
  },
  methods: {
    addDialog() {
      let character = this.characters.find(c => c.name===this.currentCharacter);
      let newDialog = {
        name: character.name,
        imgURL: character.imgURL,
        dialog: this.newDialog,
        
      };
      this.dialogs.push(newDialog);
    },
    addImage() {
      this.images.push(this.newImage);
    }
  }
});
</script>