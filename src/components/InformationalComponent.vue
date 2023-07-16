<script setup>
import {ref} from 'vue';
const emit = defineEmits(['imageSelected', 'petSelected', 'submit'])

const pet = ref()
const petsCount = ref(0)
const peopleCount = ref(0)

const imageData = ref()
const imageFileName = ref()
const imageInput = ref()

function onPetSelect() {
  if (!pet.value) {
    petsCount.value = 0
  }

  emit('petSelected', pet.value)
}

function onSelectImage() {
  const input = imageInput.value;
  const files = input.files
  if (files && files[0]) {
    const reader = new FileReader
    reader.onload = e => {
      imageData.value = e.target.result
      imageFileName.value = files[0].name
      emit('imageSelected', imageData.value)
    }
    reader.readAsDataURL(files[0])
  }
}

function onInputPeopleNumber(event) {
  console.log(event.target.value)
  if (event.target.value == '') {
    peopleCount.value = 0
    return
  }
  const value = parseInt(event.target.value)
  if (value >=0 && value <= 100) {
    peopleCount.value = value
  } else {
    event.target.value = peopleCount.value
  }
}

function onSubmit() {
  emit('submit', {pet: pet.value, petsCount: petsCount.value, peopleCount: peopleCount.value})
}
  
</script>

<template>
  <div class="personal-information">
    <form class="informations" @submit.prevent="onSubmit" :class="{'text-color-cat': pet === 'cat' , 'text-color-dog': pet === 'dog' }">
      <!--div>
        <label for="file-input">Загрузите Вашу фотографию</label>
        <input ref="imageInput" class="input-file" id="file-input" required type="file" name="photo" multiple accept="image/*,image/jpeg" @input="onSelectImage">
      </div-->
      <div class="input-file">
        <label for="file-input">
          <div class="file-input-special">Загрузите Вашу фотографию</div>
          <div class="input-file-btn">Выбрать</div>
          <div class="input-file-text"> {{ imageData ?  imageFileName : "Файл не выбран" }}</div>
        </label>
        <input ref="imageInput" class="input-file" id="file-input" required type="file" name="photo" multiple accept="image/*,image/jpeg" @input="onSelectImage">
      </div>
      <div>
        <label for="ns">Введите фамилию и имя</label>
        <input id="ns" autocomplete required type="text" name="ns" placeholder="Имя Фамилия">
      </div>
      <div>
        <label for="email">Введите email</label>
        <input id="email" required type="email" name="email" class="input" placeholder="e-mail"/>
      </div>
      <div class="information-conters">
        <div>
          <label for="pet-select">Какой питомец?(Если есть)</label>
          <select name="pets" id="pet-select" v-model="pet" @change="onPetSelect">
            <option value="">---</option>
            <option value="dog">Dog</option>
            <option value="cat">Cat</option>
          </select>
        </div>
        <div>
          <label for="pet-select" v-if="pet">Укажите количество питомцев</label>
          <select name="petsCount" id="pet-count" v-model="petsCount" v-if="pet">
            <option value="1">1</option>
            <option value="2">2</option>
          </select>
        </div>
      </div>
      <div>
        <label for="people">Сколько с Вами человек?</label>
        <input id="people" min="0" max="100" required type="number" name="people" @input="onInputPeopleNumber" :value="peopleCount">
      </div>
      <button id="form-button"><img src="@/assets/images/pngegg.png" alt="Кнопка «button»"></button>
    </form>
  </div>
</template>

<style scoped>
.informations {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.file-input-special {
  margin-bottom: 10px;
}

.information-conters {
  display: flex;
  flex-direction: column;
}

button {
  margin: 10px;
  align-self: center;
  padding: 0;
  border: 0;
  background: none;
  cursor: pointer;
}
.informations label{
  margin-bottom: 10px;
  width: 100%;
}
.informations input{
  padding: 10px 10px;
  border-radius: 6px;
	border: 1px solid #ddd;
  width: 100%;
}
.information-conters label{
  margin-bottom: 10px;
  width: 100%;
}
.information-conters select {
  padding: 8px 10px;
  border-radius: 6px;
	border: 1px solid #ddd;
  width: 100%;
}
.input-file {
	position: relative;
	display: inline-block;
}
.input-file-text {
	padding: 0 10px;
	line-height: 40px;
	text-align: left;
	height: 40px;
	display: block;
	float: right;
	box-sizing: border-box;
	width: 200px;
	border-radius: 0px 6px 6px 0px;
	border: 1px solid #ddd;
}
.input-file-btn {
  position: relative;
	display: inline-block;
	cursor: pointer;
	outline: none;
	text-decoration: none;
	font-size: 14px;
	vertical-align: middle;
	color: rgb(255 255 255);
	text-align: center;
	border-radius: 6px 0 0 6px;
	background-color: #419152;
	line-height: 22px;
	height: 40px;
	padding: 10px 20px;
	box-sizing: border-box;
	border: none;
	margin: 0;
	transition: background-color 0.2s;
}
.input-file input[type=file] {
	position: absolute;
	z-index: -1;
	opacity: 0;
	display: block;
	width: 0;
	height: 0;
}
 
/* Focus */
.input-file input[type=file]:focus + .input-file-btn {
	box-shadow: 0 0 0 0.2rem rgba(0,123,255,.25);
}
 
/* Hover/active */
.input-file:hover .input-file-btn {
	background-color: #59be6e;
}
.input-file:active .input-file-btn {
	background-color: #2E703A;
}
 
/* Disabled */
.input-file input[type=file]:disabled + .input-file-btn {
	background-color: #eee;
}
.text-color-cat {
  color: red;
}
.text-color-dog {
  color: green;
}
</style>
