<template>
  <div id="app">
    <Header @open="modalVisible = true"></Header>
    <k-table
      :persons="persons"
    ></k-table>
    <ModalWindow
      v-if="modalVisible"
      @close="modalVisible = false"
      @addNewPerson="addPerson"
      :persons="flatPersons"
    ></ModalWindow>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import KTable from './components/KTable.vue'
import ModalWindow from './components/ModalWindow.vue'

export default {
  name: 'App',
  data () {
    return {
      modalVisible: false,
      persons: [],
      flatPersons: []
    }
  },
  components: {
    Header,
    ModalWindow,
    KTable
  },
  mounted () {
    this.getPersons()
  },
  methods: {
    addChild (persons, person) {
      persons.forEach(element => {
        if (element.id === person.parent) {
          element.children = element.children || []
          element.children.push(person)
          return undefined
        } else if (element.children !== null) {
          this.addChild(element.children, person)
        }
      })
    },
    addPerson (person) {
      if (person.parent !== null) {
        this.persons.forEach(element => {
          if (element.id === person.parent) {
            element.children = element.children || []
            element.children.push(person)
            return undefined
          } else if (element.children !== null) {
            this.addChild(element.children, person)
          }
        })
      } else {
        this.persons.push(person)
      }
      this.flatPersons.push(person)
      localStorage.setItem('persons', JSON.stringify(this.persons))
      localStorage.setItem('flatPersons', JSON.stringify(this.flatPersons))
      this.getPersons()
    },
    getPersons () {
      this.persons = JSON.parse(localStorage.getItem('persons')) || []
      this.flatPersons = JSON.parse(localStorage.getItem('flatPersons')) || []
    }
  }
}
</script>

<style>
  .container {
    padding: 20px;
  }
</style>
