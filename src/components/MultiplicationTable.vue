<script setup>
import {ref} from "vue"

const name = ref('Nikolai')
const numOfRows = ref(10)
const numOfColumns = ref(10)
const rowHighlight = ref(5)
const columnHighlight = ref(5)
const showCalculations = ref(false)
</script>

<template>

  <section class="container">
    <h1 v-if="name">Hello {{ name }}!</h1>
    <h1 v-else>Hello there!</h1>

    <div class="controls">
      <label id="name">
        What's your name?
        <input id="name" type="text" v-model="name"/>
      </label>

      <label id="rows">
        <span>How many <span class="emphasis">rows</span> should we have?</span>
        <input id="rows" type="number" min="1" max="100" v-model.number="numOfRows"/>
      </label>

      <label id="columns">
        <span>How many <span class="emphasis">columns</span> should we have?</span>
        <input id="columns" type="number" min="1" max="100" v-model.number="numOfColumns"/>
      </label>

      <label id="rowHighlight">
        <span>Which <span class="emphasis">row</span> should we highlight?</span>
        <input id="rowHighlight" type="number" min="1" :max="numOfRows" v-model.number="rowHighlight"/>
      </label>

      <label id="columnHighlight">
        <span>Which <span class="emphasis">column</span> should we highlight?</span>
        <input id="columnHighlight" type="number" min="1" :max="numOfColumns" v-model.number="columnHighlight"/>
      </label>

      <label id="showCalculations">
        Should we show the math?
        <input id="showCalculations" type="checkbox" v-model="showCalculations"/>
      </label>
    </div>

    <section class="multiplication-table">

      <table>
        <tr v-for="row in numOfRows" :class="{ 'highlighted' : row === rowHighlight }">

          <td v-for="column in numOfColumns" :class="{ 'highlighted' : column === columnHighlight }">

            {{ row * column }}

            <div v-if="showCalculations" class="calculation">
              ({{ row }} * {{ column }})
            </div>

          </td>
        </tr>
      </table>

    </section>
  </section>

</template>

<style scoped>
section.container {
  font-family: Arial, Helvetica, sans-serif;
  margin: 0 auto;
  background-color: white;
  padding: 10px;
  border: 10px solid black;
  display: flex;
  flex-direction: column;
  align-items: center;

  h1 {
    margin-top: 0;
  }

  div.controls {
    display: flex;
    flex-direction: column;
    row-gap: 20px;
    column-gap: 20px;
    margin-bottom: 30px;

    > label {
      display: flex;
      justify-content: space-between;
      column-gap: 20px;
      align-items: center;

      span.emphasis {
        font-style: italic;
      }
    }

    input {
      font-size: 1rem;

      &[type='text'] {
        text-align: center;
      }
    }
  }

  section.multiplication-table {
    table {
      background-color: lightgray;
      border-collapse: collapse;

      tr {
        &.highlighted {
          background-color: red;
          color: white;
        }

        td {
          text-align: center;
          padding: 0.5rem;

          &.highlighted {
            background-color: red;
            color: white;
          }

          .calculation {
            font-size: 0.7rem;
          }
        }
      }
    }
  }
}
</style>