<template>
  <div class="container">
    <div class="table">
      <tr class="table__header">
        <th class="header">
          <h2>ID</h2>
           <button @click="sortId" class="arrow__sort down"></button>
          <button @click="unSortId" class="arrow__sort up"></button>
        </th>
        <th class="header">
          <h2>Имя</h2>
          <button @click="sortName" class="arrow__sort down"></button>
          <button @click="unSortName" class="arrow__sort up"></button>
        </th>
        <th class="header">
          <h2>Телефон</h2>
          <button @click="sortPhone" class="arrow__sort down"></button>
          <button @click="unSortPhone" class="arrow__sort up"></button>
        </th>
        <th class="header">
          <h2>Родитель</h2>
        </th>
      </tr>
      <keep-alive
        v-for="(item) in persons"
        :key="item.phone"
      >
        <BodyTable
          :person="item"
          :paddingLeft="5"
        ></BodyTable>
      </keep-alive>
    </div>
  </div>
</template>

<script>
import BodyTable from '@/components/BodyTable.vue'

export default {
  name: 'KTable',
  data: () => ({
  }),
  props: ['persons'],
  components: {
    BodyTable
  },
  methods: {
    childrenSort (children, sort) {
      children.map(child => {
        if (child.children && child.children.length) {
          this.childrenSort(child.children, sort)
        }
      })
      children.sort(sort)
    },
    sortId () {
      this.childrenSort(this.persons, function (a, b) {
        return a.id - b.id
      })
    },
    unSortId () {
      this.childrenSort(this.persons, function (a, b) {
        return b.id - a.id
      })
    },
    sortName () {
      this.childrenSort(this.persons, function (a, b) {
        let nameA, nameB
        nameA = a.name.toLowerCase()
        nameB = b.name.toLowerCase()

        if (nameA < nameB) return -1
        if (nameA > nameB) return 1
        return 0
      })
    },
    unSortName () {
      this.childrenSort(this.persons, function (a, b) {
        let nameA, nameB
        nameA = a.name.toLowerCase()
        nameB = b.name.toLowerCase()

        if (nameA < nameB) return 1
        if (nameA > nameB) return -1
        return 0
      })
    },
    sortPhone () {
      this.childrenSort(this.persons, function (a, b) {
        let phoneA, phoneB
        phoneA = a.phone.toLowerCase()
        phoneB = b.phone.toLowerCase()

        if (phoneA < phoneB) return -1
        if (phoneA > phoneB) return 1
        return 0
      })
    },
    unSortPhone () {
      this.childrenSort(this.persons, function (a, b) {
        let phoneA, phoneB
        phoneA = a.phone.toLowerCase()
        phoneB = b.phone.toLowerCase()

        if (phoneA < phoneB) return 1
        if (phoneA > phoneB) return -1
        return 0
      })
    }
  }
}
</script>

<style>
  .container {
    padding: 20px;
  }

  .table {
    width: 100%;
    font-size: 14px;
    border-radius: 10px;
    border-spacing: 0;
    text-align: center;
  }

  .table__header {
    display: flex;
    flex-direction: row;
    width: 100%;
  }

  .header:first-child {
    width: 10%;
  }

  .header {
    width: 45%;
    padding: 5px 10px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .arrow__sort:first-child {
    margin-left: 5px;
  }

  .arrow__sort{
    border: none;
    padding: 1px;
    border-radius: 50%;
    margin: 0px;
    cursor: pointer;
    height: 25px;
    width: 25px;
  }

  .down {
    margin-left: 5px;
    background: url(../assets/arrow-down-drop-circle-outline.svg);
  }

  .up {
    background: url(../assets/arrow-up-drop-circle-outline.svg);
  }

  .arrow__sort:first-child {
    margin-left: 10px;
  }

  .arrow__sort:hover {
    opacity: 0.5;
  }
</style>
