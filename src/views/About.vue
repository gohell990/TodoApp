<template>
  <div class="about">
    <v-text-field
      v-model="textTitle"
      @click:append="addTask"
      @keyup.enter="addTask"
      class="pa-3"
      outlined
      label="Add Task"
      append-icon="mdi-plus"
      hide-details
      clearable
    ></v-text-field>

    <v-list
    
      two-line
      flat
      class="pt-0"
    >
      
      <div  v-for="task in tasks"
            :key="task.id">
        <v-list-item-group
          v-model="settings"
          multiple       
        >
          <v-list-item
           @click="doneTask(task.id)"
           :class="{'cyan accent-2' : task.done}"
           
          >
            <template v-slot:default>
              <v-list-item-action>
                <v-checkbox
                  :input-value="task.done"
                  color="primary"
                ></v-checkbox>
              </v-list-item-action>

              <v-list-item-content>
                <v-list-item-title
                :class="{'text-decoration-line-through' : task.done}">
                  {{task.name}}
                </v-list-item-title>
                
              </v-list-item-content>

              <v-list-item-action>
              <v-btn 
                @click.stop="deleteTask(task.id)"
                icon
              >
                <v-icon color="primary lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>           
            </template>
 
          </v-list-item>
        </v-list-item-group>

        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  
  name: "About",
  data() {
    return {
      textTitle: '',
      tasks:[
        // {id:1, name:"Wake up", done:true},
        // {id:2, name:"Breakfast", done:false},
        // {id:3, name:"Noon", done:false},
        // {id:4, name:"Nap", done:false},
      ]
    }
  },
  methods:{
    addTask(){
      let task = {
        id: Date.now(),
        name: this.textTitle,
        done:false,
      }
      this.tasks.push(task)

      this.textTitle = ''
      this.textTitle = ''
    },
    doneTask(id){
      let task = this.tasks.filter(task => task.id === id)[0]
      task.done = !task.done
    },
    deleteTask(id){
      this.tasks = this.tasks.filter(task => task.id !== id)
    }
  }
}
</script>
