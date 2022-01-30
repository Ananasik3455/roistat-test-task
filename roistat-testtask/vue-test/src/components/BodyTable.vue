<template>
  <div class="container">
      <tr class="table__body">
        <td class="body">
          <h3 class="id__item" :style="{ paddingLeft: paddingLeft + 'px' }">{{ person.id+1 }}</h3>
          <button
            v-show="person.children !== null"
            class="arrow"
            @click.stop="unVisible"
            :class="visibility ? 'up' : 'down'"
          ></button>
        </td>
        <td class="body">
          <h3>{{ person.name }}</h3>
        </td>
        <td class="body">
          <h3>{{ person.phone }}</h3>
        </td>
        <td class="body">
          <h3 v-if="parentName">{{ parentName }}</h3>
          <h3 v-else>-</h3>
        </td>
      </tr>
      <div class="table__child">
        <keep-alive
          v-for="(child) in person.children"
          :key="child.phone"
        >
          <BodyTable
            class="body__child"
            v-show="visibility"
            :person="child"
            :parentName="person.name"
            :paddingLeft= "paddingLeft + 10"
          >
          </BodyTable>
        </keep-alive>
      </div>
  </div>
</template>

<script>
export default {
  name: 'BodyTable',
  data: () => ({
    visibility: false
  }),
  props: ['person', 'paddingLeft', 'parentName'],
  methods: {
    unVisible () {
      this.visibility = !(this.visibility)
    }
  }
}
</script>

<style>
  .container {
    margin: 0;
    padding: 0;
    min-width: 100%;
  }

  .arrow {
    margin-left: 10px;
    background: none;
    border: none;
    height: 25px;
    width: 25px;
  }

  .arrow:hover {
    opacity: 0.5
  }

  .table__body {
    display: flex;
    flex-direction: row;
    width: 100%;
  }

  .table__child {
    width: 100%;
  }

  .body:first-child {
    width: 10%;
    display: flex;
  }

  .body {
    width: 45%;
    padding: 5px 10px;
  }

  .body__child .id__item {
    padding-left: 10px;
  }

  .down {
    background: url(../assets/arrow-down-drop-circle-outline.svg);
  }

  .up {
    background: url(../assets/arrow-up-drop-circle-outline.svg);
  }

  th {
    background: #88e2c7;
    color: white;
    text-shadow: 0 1px 1px #2D2020;
    padding: 10px 20px;
  }

  th, td {
    border-style: solid;
    border-width: 0 1px 1px 0;
    border-color: white;
  }

  th:first-child, td:first-child {
    text-align: left;
  }

  th:first-child {
    border-top-left-radius: 10px;
  }

  th:last-child {
    border-top-right-radius: 10px;
    border-right: none;
  }

  td {
    padding: 10px 20px;
    background: #c6f1e4;
  }

  tr:last-child td:first-child {
    border-radius: 0 0 0 10px;
  }

  tr:last-child td:last-child {
    border-radius: 0 0 10px 0;
  }

  tr td:last-child {
    border-right: none;
  }

</style>
