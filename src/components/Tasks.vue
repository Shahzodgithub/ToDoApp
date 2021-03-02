<template>
  <div class="tasks-board">
    <div class="card">
      <h4>
        {{ title }}
        <div class="dots" @click="isModalOpen = !isModalOpen">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </h4>

      <div class="list" >
        <ul v-for="(text, index) in addTextValue" :key="index"
        id="list-`${index}`"
        @dragover.prevent
        @drop.stop="drop"
        ><slot/>
          <li class="card-list card" id="card-`${index}`"
          :draggable="draggable"
          @dragstart="dragStart"
          @dragover.stop>
          <slot/>
            <div>
              {{ text }}
            </div>
            <button class="btn danger" @click="deleteCard(index)">X</button>
          </li>
        </ul>
        <p v-show="addTextValue == []">Here is no any tasks yet</p>
      </div>
      <textarea cols="30" rows="5" v-model="textValue"></textarea>
      <button class="btn" @click="addCard" :disabled="textValue.trim() == ''">
        Add a card
      </button>
    </div>
    <div class="card" v-if="isModalOpen">
      <span class="label">Position</span
      ><span class="value">{{selectedM}}</span>
      <select v-model="selectedM">
        <option>1</option>
        <option>2</option>
        <option>3</option>
        <option>3</option>
      </select>
      <input class="nch-button" type="submit" value="Move" @click="moveTask" />
    </div>
  </div>
</template>

<script>
export default {
  props: ["title", "selected", "id"],
  data() {
    return {
      textValue: "",
      addTextValue: [],
      isModalOpen: false,
      selectedM: '1',

    };
  },
  methods: {
    addCard() {
      this.addTextValue.push(this.textValue);
      this.textValue = "";
    },
    deleteCard(index) {
      this.addTextValue.splice(index, 1);
    },
    moveTask(){
        this.textValue = "";
        this.addTextValue.push(this.textValue);
    },
    drop(e){
        const card_id = e.dataTransfer.getData('card_id');

        const card = document.getElementById(card_id)

        card.style.display = 'block'

        e.target.appendChild(card)
    },
    dragStart(e){
        const target = e.target;

        e.dataTransfer.setData('card_id', target.id)

        setTimeout(() => {
            target.style.display = 'none'
        }, 0);
    }
  },
};
</script>

<style scoped>
.card-list {
  width: 218px;
  padding: 5px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.list {
  width: 230px;
  margin: auto;
}

.danger {
  display: block;
}
.tasks-board {
  margin: auto;
  /* display: flex;
  justify-content: space-between; */
}
textarea {
  margin: 20px 0;
  width: 100%;
  border-radius: 5px;
  height: auto;
  overflow-y: auto;
  padding: 0;
}

.nch-button{
    width: 60px;
    display: block;
    margin: auto;
    padding: 4px !important;
    font-size: 12px !important;
    font-weight: 400 !important;
    border-radius: 15px;
}

.nch-button:focus{
    border: none;
}


ul {
  display: block;
  margin-inline-start: 0px;
  margin-inline-end: 0px;
  padding-inline-start: 0px !important;
  line-height: 0;
}

ul li {
  display: block;
  border-radius: 4px;
  border: 1px solid #000;
  background-color: #eee;
  margin-bottom: 10px;
}

.card {
  margin-top: 0;
}

h4 {
  position: relative;
}

.dots {
  position: absolute;
  top: 13%;
  right: 1%;
  width: 14px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
}

.dots span {
  display: block;
  height: 3px;
  width: 3px;
  background-color: #052;
  border-radius: 50%;
}
</style>



