<template>
  <v-app>
    <v-container grid-list-xl>
      <v-dialog v-model="dialog" max-width="500px">
        <v-card>

          <div class="title">                      
            <v-text-field 
            placeholder= "Title..." 
            type="title" 
            v-model="current_title"
            full-width>
          </v-text-field>
        </div>
        <v-text-field
        v-model="current_text" 
        name="poem-input"
        placeholder="Write here"
        single-line
        multi-line
        auto-grow
        full-width
        value="current_text"
        class="input">
        
      </v-text-field>
      <span><v-btn @click.prevent="editNote" flat >Done</v-btn>
        <v-btn color="primary" flat @click.prevent="closeEdit()">Close</v-btn>
      </span>
      
    </v-card>
  </v-dialog>
  
  <v-layout row wrap align-center>
    <v-flex xs6 offset-xs3>
     <v-card b80 >
      <v-form @submit.prevent >  
        <div class="title">                      
          <v-text-field 
          placeholder= "Title..." 
          type="title" 
          v-model="title"
          full-width>
        </v-text-field>
      </div>
      <v-text-field v-model="text"
      name="poem-input"
      placeholder="Write here"
      single-line
      multi-line
      auto-grow
      full-width
      class="input">
    </v-text-field>
    <span><v-btn @click.prevent="addNote"  flat >Done</v-btn></span>
  </v-form>
  
</v-card>
</v-flex>
<v-flex xs6 offset-xs3 v-for="item in notes" :key=item>
  <v-card 
  @dblclick="edit(item)">
  <v-card-title>
    <div class="title">{{item.title}}</div>
  </v-card-title>
  <v-card-text> 

    <p class="text-lg-left">{{item.note}}</p>
  </v-card-text>
  <v-card-actions>
    <v-btn small flat v-on:click="edit(item)" >
      Edit
    </v-btn>
    <v-btn small flat v-on:click="deleteNote(item.id)" >
      Delete
    </v-btn>
  </v-card-actions>
</v-card>
</v-flex>
</v-layout>
</v-container>
</v-app>
</template>
<script>
import axios from 'axios';
export default {
 name: 'Main',
 data () {
   return {
     items: [],
     title: '',
     text: '',
     show: 'all',
     drag: {},
     dialog: false,
     current_text:'',
     current_title:'',
     current_id: null,
     item_id: 0,
     temp_item:{}
     
   }
 },

 created: function() {
   this.$store.dispatch('getNotes');
 },
 computed: {
  notes: function(){
    return this.$store.getters.notes;
  }
 },
 methods: {
    getNotes: function(){
   this.$store.dispatch('getNotes');
  },
  addNote: function() {
       this.$store.dispatch('addNote',{
         note: this.text,
         title: this.title,
       }).then(note => {
   this.text = "";
   this.title= "";
       });
     },

  deleteNote: function(note_id) {
    this.$store.dispatch('deleteNote',
    note_id

    ).then(
    this.$store.dispatch('getNotes'));
  },
  editNote: function() {
    console.log("got to editNote")
    console.log("curr_title:", this.current_title);
    console.log("curr_text", this.current_text);

    this.$store.dispatch('updateNote',
    [this.current_id, {
      title: this.current_title,
      note: this.current_text,}
      ]
    ).then(
    this.$store.dispatch('getNotes')
    ).then(this.closeEdit());
  },

edit: function(item){
 
 this.current_text= item.note;
 this.current_title=item.title;
 this.current_id=item.id;
 this.dialog=true;
 this.temp_item=item;
},

closeEdit:function(){
 this.current_text="";
 this.current_title="";
 this.current_id=null;
 this.dialog=false;
}
},

}
</script>
<style scoped>
.title{
  font-size:3em;
  font-weight: bold;
}
.headline{
  font-size: 1.5em;
}
ul {
 list-style: none;
}

li {
 width: auto;
 min-height: 40px;
 padding-left: 10px;
 margin-bottom: 3px;
 font-size: 1em;
 display: flex;
 align-items: center;
 
}

.delete {
 display: none;
 margin-left: auto;
}

li:hover .delete {
 display: block;
}

label {
 width: 400px;
}
.text-lg-left{
  
  padding-left: 20px;
}
</style>