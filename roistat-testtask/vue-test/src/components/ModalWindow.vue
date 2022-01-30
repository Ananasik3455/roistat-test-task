<template>
    <div>
      <div class="modal-backdrop" @click="$emit('close')"></div>
      <div class="modal">
          <form class="form-control" @submit.prevent="submitForm">
              <h1>Добавление пользователя</h1>
              <input
                v-model="nameInput"
                type="text"
                placeholder="Введите имя"
              >
              <phone-mask-input
                v-model="phoneInput"
                autoDetectCountry
              />
              <select
                v-model="parentId"
              >
                <option
                  v-if="!persons || persons.length == 0"
                >
                  Отсутствуют данные о родителе
                </option>
                <option v-else
                  v-for="(item, idx) in persons"
                  :key="item.phone + idx"
                  :value="idx"
                >
                  {{ item.name }}
                </option>
              </select>
              <button class="submit">Добавить пользователя</button>
              <label class="error">{{ error }}</label>
          </form>
      </div>
    </div>
</template>

<script>
import PhoneMaskInput from 'vue-phone-mask-input'

export default {
  data () {
    return {
      nameInput: '',
      phoneInput: '',
      parentId: null,
      error: ''
    }
  },
  props: ['persons'],
  emits: ['close'],
  methods: {
    submitForm () {
      if (this.nameInput.length > 2 && this.phoneInput.length > 11) {
        this.error = ''
        this.$emit('addNewPerson', {
          id: this.persons.length,
          name: this.nameInput,
          phone: this.phoneInput,
          parent: this.parentId,
          children: null
        })
        this.$emit('close')
      } else {
        this.error = 'Не все поля заполнены'
      }
    }
  },
  components: {
    PhoneMaskInput
  }
}
</script>

<style scoped>
  .error {
    font-size: 10px;
    color: red;
    display: block;
  }

  .modal {
    position: fixed;
    top: 160px;
    min-height: 200px;
    width: 500px;
    padding: 20px;
    background: #fff;
    z-index: 1000;
    left: 50%;
    border-radius: 10px;
    transform: translateX(-50%);
    box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.2);
    text-align: center;
  }

  .modal-backdrop {
    position: fixed;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    background: rgba(0, 0, 0, .35);
  }

  .form-control {
    position: relative;
    margin-bottom: 10px;
  }

  .form-control input {
    margin: 15px auto;
    outline: none;
    border: 2px solid #ccc;
    display: block;
    width: 80%;
    color: #2c3e50;
    padding: 10px 20px;
    border-radius: 3px;
    font-size: 15px;
    resize: none;
  }

  .form-control select {
    margin: 25px auto;
    outline: none;
    border: 2px solid #ccc;
    display: block;
    width: 88%;
    color: #2c3e50;
    padding: 10px 20px;
    border-radius: 3px;
    font-size: 15px;
    resize: none;
  }

  .form-control input:active,
  .form-control input:focus {
    transition: border 0.22s;
    border: 2px solid #42b983;
  }

  .submit {
    border: 2px solid #08786C;
    font-size: 14px;
    border-radius: 10px;
    background: #3fbd97;
    text-shadow: 0 1px 1px #2D2020;
    border-spacing: 0;
    transition: all 0.3s ease-in-out;
    color: #FFFFFF;
    text-decoration: none;
    padding: 5px 20px;
    cursor: pointer;
  }

  .submit:hover {
    border-color:#05574f;
    background: #0aa394;
    transition: all 0.3s ease-in-out;
  }
</style>
