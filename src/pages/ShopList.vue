<template>
  <q-page class="flex flex-top-left ">
    <div class="q-pa-md">

      <q-form
        @submit.prevent="saveItem"
        class="q-gutter-md"
      >
        <q-input
         filled
          v-model.trim="newItem"
          type="text"
          label="Item"
          lazy-rules
          :rules="[ val => val && val.length > 1 || 'Please type something']"
        />

        <q-toggle v-model="newItemHighPrio" label="High Priority" />

        <div>
          <q-btn label="Submit" type="submit" color="primary"/>
          <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
        </div>
      </q-form>

      <div class="q-pa-md, list">
        <q-list bordered separator>
          <q-slide-item
          v-for="(item, index) in items"  :key="item"
          @left="deleteItem(index)" 
          :class="[{prioStyle: item.highPrio}]"
          >
          <q-slide-item>
            <q-avatar>
            </q-avatar>
              {{ item.id }}
              {{ item.text }} 
            <template v-slot:left>
              <q-icon name="done" />
              {{ item.text }}
            </template>
          </q-slide-item>
          </q-slide-item>
        </q-list>
      </div>

    </div>
  </q-page>
</template>
  
<script setup>
  import { ref, } from 'vue'
  import { useQuasar } from 'quasar'


  const newItem = ref("")
  const newItemHighPrio = ref(false)
  const $q = useQuasar()

  let items = ref([
                      {
                        id: 1, 
                        text: "hatter",
                        //purchased: false,
                        highPrio: false,
                      },
                      {
                        id: 2,
                        text: "sko",
                       // purchased: true,
                        highPrio: true
                      }
  ])
  const saveItem = ()=>{
    items.value.push({id: items.value.length + 1, text: newItem.value, purchased: false, highPrio: newItemHighPrio.value})                     
    newItem.value = ""
  }

  function deleteItem(index) { console.log("kfesfsofkse")
    $q.this.items.value = this.items.value.splice(index, 1); 
  }


</script>

<style scoped>

  .prioStyle {
    color: red;
  }
  
  .deleteStyle {
    display: none;
  }

  .list {
    width: 30rem;
    border-radius: 10rem;
  }
  
  .listItem {
    height: 6rem;
  }
</style>
  