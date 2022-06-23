<template>
    <div class="container">
      <div class="content" v-for="(grades, subject) in subjects" :key="subject">
        <div class="subject">{{ subject }}</div>
        <br>
        <div class="grade" v-for="(grade, index) in grades.grades" :key="index">
          <div>
            {{ parseFloat(grade).toFixed(2) }}
            <button @click="deletegrade(subject, index)">❌</button>
          </div><br>          
        </div>
        <br>
        <div class="grade-add"><input type="number" min="0" max="6" @keyup.enter="addgrade($event, subject)" /></div>
        <br>
        <br>
        <div class="grade-average">Ø: {{ parseFloat(calcAverageGrade(subject)).toFixed(2) }}</div>
      </div>
    </div>
    <table>
      <tbody>
        <tr>
          <td>
            <label type="text">New Subject: </label>
            <input type="text" @keyup.enter="addNewSubject($event)"/>
          </td>
        </tr>
        <tr>
          <td>Average Ø</td>
          <td>{{ parseFloat(roundHalf(calcAverageGradeForAllSubjects())).toFixed(2) }}</td>
        </tr>
      </tbody>
    </table>
</template>

<script setup>

import { ref } from "@vue/reactivity";

const subjects = ref({
    PE:       { grades: [6] },
    Physics:  { grades: [4.5] },
    Music:    { grades: [6, 6] },
    IT:       { grades: [6, 6] },
    Math:     { grades: [4, 5.5] },
    Finance:  { grades: [2, 5, 4] },
    English:  { grades: [6, 6] },
});

function deletegrade(subject, grade) {
    subjects.value[subject].grades.splice(grade, 1);
}

function addgrade(e, subject) {
    let newgrade = Math.min(6, Math.max(1, parseInt(e.target.value)));

    subjects.value[subject].grades.push(newgrade);
}

function calcAverageGrade(subject) {
    let sum = 0;

    for (let grade of subjects.value[subject].grades) {
        sum += grade;
    }

    return sum / subjects.value[subject].grades.length;
}

function calcAverageGradeForAllSubjects() {
    let sum = 0;
    let count = 0;

    for (let subject in subjects.value) {
        for (let grade of subjects.value[subject].grades) {
            sum += grade;
            count++;
        }
    }

    return sum / count;
}

function addNewSubject(e) {
    subjects.value[e.target.value] = { grades: [] };
}

function roundHalf(num) {
    return Math.round(num*2)/2;
}

</script>

<style>

.home {
    margin: 0;
    display: grid;
    min-height: 100vh;
    min-width: 100vw;
    justify-content: center;
}

ul#subjects {
    width: 50%;
}

</style>