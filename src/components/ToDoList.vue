<template lang="html">

<span class="">
  <input type="submit" name="" value="open" @click="isVisible=true" v-if="!isVisible">
  <input type="submit" name="" value="close" @click="isVisible=false" v-if="isVisible">

<div id="app">

<div class="container" v-if="isVisible">

  <div v-if="!isEditing">
    <input type="text" v-model="goal" @keyup.enter="addGoal">
    <input type="submit" value="add" @click="addGoal">
  </div>

  <div v-else>
    <input type="text" v-model="goal" @keyup.enter="updateGoal">
    <input type="submit" value="update" @click="updateGoal">
  </div>

  <ol v-if="goals.length != 0">
    <li v-for="(goal, index) in goals">
      {{ goal }}
      <button type="button" name="button" @click="editGoal(index, goal)">Edit</button>
      <button type="button" name="button" @click="deleteGoal(index)">Delete</button>
    </li>
  </ol>

</div>

</div>

</span>


</template>

<script>
export default {
  data: function() {
    return {
      goal: '',
      isEditing: false,
      editingIndex: null,
      isVisible: false,
    };
  },
  props: ["goals"],

  methods: {

    addGoal: function() {
      if (this.goal == '') {
        return;
      }
      this.goals.push(this.goal);
      this.goal = '';
    },

    editGoal: function(index, goal) {
      this.goal = goal;
      this.isEditing = true;
      this.editingIndex = index;
    },

    deleteGoal: function(index) {
      this.goal = '';
      this.isEditing = false;
      this.editingIndex = null;
      this.goals.splice(index, 1);
    },

    updateGoal: function() {
      if (this.goal == '') {
        this.deleteGoal(this.editingIndex);
      } else {
        this.goals[this.editingIndex] = this.goal;
      }
      this.goal = '';
      this.isEditing = false;
      this.editingIndex = null;
    }
  },
}
</script>

<style lang="css" scoped>
</style>
