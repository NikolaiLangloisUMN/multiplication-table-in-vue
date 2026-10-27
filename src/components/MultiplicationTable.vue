<script setup>
import {computed, ref} from "vue"
import InputField from "./InputField.vue";

const firstName = ref(null)
const lastName = ref(null)
const numOfRows = ref(10)
const numOfCols = ref(10)
const rowHighlight = ref(5)
const colHighlight = ref(5)
const showCalculations = ref(false)
const calculatedResult = ref(null)

const fullName = computed(() => {
  if (firstName.value && lastName.value) {
    return `${ firstName.value } ${ lastName.value }`
  } else if (firstName.value && !lastName.value) {
    return firstName.value
  } else if (!firstName.value && lastName.value) {
    return lastName.value
  } else {
    return ' there'
  }
})

const calculateValue = (row, col) => {
  let value = row * col
  calculatedResult.value = `${ row } * ${ col } = ${ value }`
}
</script>

<template>

  <section class="container">
    <h1>Hello {{ fullName }}!</h1>

    <div class="controls">
      <input-field v-model="firstName"
                   label-copy="What's your <em>first name</em>?"
                   type="text"
                   name="first-name"/>

      <input-field v-model="lastName"
                   label-copy="What's your <em>last name</em>?"
                   type="text"
                   name="last-name"/>

      <input-field v-model="numOfRows"
                   label-copy="How many <em>rows</em> should we have?"
                   type="number"
                   name="num-of-rows"
                   min="1" max="40"/>

      <input-field v-model="numOfCols"
                   label-copy="How many <em>columns</em> should we have?"
                   type="number"
                   name="num-of-cols"
                   min="1" max="40"/>

      <input-field v-model="rowHighlight"
                   label-copy="Which <em>row</em> should we highlight?"
                   type="number"
                   name="row-highlight"
                   min="1" :max="numOfRows.toString()"/>

      <input-field v-model="colHighlight"
                   label-copy="Which <em>column</em> should we highlight?"
                   type="number"
                   name="col-highlight"
                   min="1" :max="numOfCols.toString()"/>

      <input-field v-model="showCalculations"
                   label-copy="Should we show the math?"
                   type="checkbox"
                   name="show-calculations"
                   min="1" :max="numOfCols.toString()"/>

      <p v-if="showCalculations && calculatedResult" v-text="calculatedResult"/>
    </div>


    <section class="multiplication-table">

      <table>
        <tr v-for="row in numOfRows"
            :class="{ 'highlighted' : row === rowHighlight }">

          <td v-for="column in numOfCols"
              :class="{ 'highlighted' : column === colHighlight }"
              @click="calculateValue(row, column)">

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
  max-width: 90vw;

  h1 {
    margin-top: 0;
  }

  div.controls {
    display: flex;
    flex-direction: column;
    row-gap: 20px;
    column-gap: 20px;
    margin-bottom: 30px;
  }

  section.multiplication-table {
    overflow-x: scroll;
    max-width: 100%;

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
            white-space: nowrap;
          }

          &:hover {
            cursor: pointer;
            border: 1px solid black;
          }
        }
      }

      tr.highlighted > td.highlighted {
        font-weight: bold;
        color: black;
        font-size: 115%;
      }
    }
  }
}
</style>