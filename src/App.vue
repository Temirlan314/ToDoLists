<template lang="html">

<div class="container">
  <h1>Your ToDoList List</h1>

  <button type="button"  @click="addingNewList = true" v-if="!addingNewList && !isEditingList">Add a new To Do List</button>

  <div v-if="addingNewList">
    <input type="text" v-model="newListTitle" @keyup.enter="addList">
    <input type="submit" value="Add" @click="addList">
    <input type="submit" value="Cancel" @click="newListTitle=''; addingNewList=false">
  </div>

  <div v-if="isEditingList">
      <input type="text" v-model="newListTitle" @keyup.enter="updateTitle">
      <input type="submit" value="Update" @click="updateTitle">
      <input type="submit" value="Cancel" @click="cancellingEdit">
  </div>

  <br v-if="!addingNewList && !isEditingList">
  <br v-if="!addingNewList && !isEditingList">

  <ul>
    <li v-for="(listName, index) in listNames">
      {{listName}}
      <input type="submit" @click="editTitle(index)" value="edit">
      <input type="submit" @click="deleteList(index)" value="delete">
      <appList :goals="lists[index]"></appList>

    </li>
  </ul>

</div>

</template>

<script>
import List from "./components/ToDoList.vue"

export default {
  components: {
    appList: List,
  },

  data: function() {
    return {
      listNames: ["Work", "Hobby"],
      lists: [
        [],
        []
      ],
      addingNewList: false,
      newListTitle: "",

      isEditingList: false,
      editingListIndex: null,

    };
  },
  methods: {
    addList() {
      if (this.newListTitle == '') {
        return;
      }
      this.lists.push([]);
      this.listNames.push(this.newListTitle);
      this.newListTitle = '';
    },

    deleteList(index) {
      this.newListTitle = '';
      this.isEditingList = false;
      this.editingListIndex = null;
      this.lists.splice(index, 1);
      this.listNames.splice(index, 1);
    },

    editTitle(index) {

      this.newListTitle = this.listNames[index];
      this.isEditingList = true;
      this.editingListIndex = index;
      this.addingNewList = false;
    },

    updateTitle() {
      if (this.newListTitle == '') {
        this.deleteList(this.editingListIndex);
      } else {
        this.listNames[this.editingListIndex] = this.newListTitle;
      }
      this.newListTitle = '';
      this.isEditingList = false;
      this.editingListIndex = null;
    },

    cancellingEdit() {
      this.newListTitle = '';
      this.isEditingList = false;
      this.editingListIndex = null;
    }
  }
}
</script>

<style lang="css">
.container {
  max-width: 960px;
  margin: 0 auto;
}

h1 {
  padding-top: 40px;
}

ol {
  border: 2px solid rgb(155, 77, 202, 0.5);
  border-radius: 15px;
  padding: 20px;
}

</style>
