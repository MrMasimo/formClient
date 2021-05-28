<template>
  <form class="wrapper">
    <h2>Карта клиента</h2>
    <div class="form-common-info">
      <div class="form-header">Общая информация</div>
      <div class="form-flex">
        <!-- Фамилия клиента -->
        <div class="form-group">
        <i class="icon-required">*</i>
        <label for="surname">Фамилия</label><br>
        <input @blur="$v.formReg.surname.$touch()"
          :class="status($v.formReg.surname)"
          v-model.trim="formReg.surname"
          type="text" class="form-control" id="surname" placeholder="Иванов"><br>
        <span class="invalid-feedback" v-if="!$v.formReg.surname.required && $v.formReg.surname.$dirty">Не заполнено</span><br>
        <span class="invalid-feedback" v-if="!$v.formReg.surname.alpha && $v.formReg.surname.$dirty">Запрещены цифры, пробелы и другие символы</span>
        </div>
        <!-- Имя клиента -->
        <div class="form-group">
          <i class="icon-required">*</i>
          <label for="name">Имя</label><br>
          <input @blur="$v.formReg.name.$touch()"
            :class="status($v.formReg.name)"
            v-model.trim="formReg.name"
            type="text" class="form-control" id="name" placeholder="Иван"><br>
          <span class="invalid-feedback" v-if="!$v.formReg.name.required && $v.formReg.name.$dirty">Не заполнено</span><br>
          <span class="invalid-feedback" v-if="!$v.formReg.name.alpha && $v.formReg.name.$dirty">Запрещены цифры, пробелы и другие символы</span>
        </div>
        <!-- Отчество клиента -->
        <div class="form-group">
          <label for="fatherName">Отчество</label><br>
          <input 
            v-model.trim="formReg.fatherName"
            type="text" class="form-control" id="fatherName"><br>
        </div>
        <!-- Дата рождения -->
        <div class="form-group">
          <i class="icon-required">*</i>
          <label for="birth">Дата рождения</label><br>
          <input @blur="$v.formReg.birth.$touch()"
            :class="status($v.formReg.birth)"
            v-model.trim="formReg.birth"
            type="text" class="form-control" id="birth" placeholder="YYYY-MM-DD"><br>
          <span class="invalid-feedback" v-if="!$v.formReg.birth.required && $v.formReg.birth.$dirty">Не заполнено</span><br>
          <span class="invalid-feedback" v-if="!$v.formReg.birth.date && $v.formReg.birth.$dirty">Проверьте формат даты</span>
        </div>
        <!-- Телефон -->
        <div class="form-group">
          <i class="icon-required">*</i>
          <label for="phone">Телефон</label><br>
          <input @blur="$v.formReg.phone.$touch()"
            :class="status($v.formReg.phone)"
            v-model.trim="formReg.phone"
            type="tel" class="form-control" id="phone" placeholder="79995553322"><br>
          <span class="invalid-feedback" v-if="!$v.formReg.phone.required && $v.formReg.phone.$dirty">Не заполнено</span><br>
          <span class="invalid-feedback" v-if="!$v.formReg.phone.phone&& $v.formReg.phone.$dirty">Номер должен начинаться с 7 и состоять из 11 цифр</span>         
        </div>
        <!-- Пол -->
        <div class="form-group">
          <label for="gender">Пол</label><br>
          <select 
            v-model="formReg.gender"
            class="select-control" id="gender" size="1">
              <option></option>
              <option>Мужской</option>
              <option>Женский</option>
          </select>
        </div>
      </div>
      <div class="form-flex">
        <!-- Категория клиента -->
        <div class="form-group">
          <i class="icon-required">*</i>
          <label for="groupClient">Группа клиентов</label><br>
          <select @blur="$v.formReg.groupClient.$touch()"
            :class="status($v.formReg.groupClient)"
            v-model="formReg.groupClient"
            class="multyselect-control" id="groupClient" multiple>
              <option>VIP</option>
              <option>Проблемные</option>
              <option>ОМС</option>
            </select>
            <br>
          <span class="invalid-feedback" v-if="!$v.formReg.groupClient.required && $v.formReg.groupClient.$dirty">Не выбран</span><br>
        </div>
         <!-- Лечащий врач -->
        <div class="form-group">
          <label for="doctor">Лечащий врач</label><br>
          <select 
            v-model.trim="formReg.doctor"
            class="select-control" id="doctor" size="1">
              <option></option>
              <option>Иванов</option>
              <option>Захаров</option>
              <option>Чернышева</option>
            </select>
        </div>
      </div>
      <!-- Отказ от СМС -->
      <div class="form-group">
        <input class="checkBox-control" type="checkbox" v-model="formReg.isSms" id="isSms">
        <label  for="isSms">Не отправлять СМС</label>
      </div>
    </div>

    <div class="form-address-info">
      <div class="form-header">Адрес</div>
      <div class="form-flex">
        <!-- Индекс -->
        <div class="form-group">
        <label for="index">Индекс</label><br>
        <input @blur="$v.formAddress.index.$touch()"
          :class="status($v.formAddress.index)"
          v-model.trim="formAddress.index"
          type="text" class="form-control" id="index"><br>
        <span class="invalid-feedback" v-if="!$v.formAddress.index.index && $v.formAddress.index.$dirty">Допускаются цифры в колличестве 6 штук</span><br>
        </div>
        <!-- Страна -->
          <div class="form-group">
            <label for="country">Страна</label><br>
            <input 
              v-model.trim="formAddress.country"
              type="text" class="form-control" id="country"><br>
        </div>
        <!-- Область -->
        <div class="form-group">
          <label for="area">Область</label><br>
          <input 
            v-model.trim="formAddress.area"
            type="text" class="form-control" id="area"><br>
        </div>
        <!-- Город -->
        <div class="form-group">
          <i class="icon-required">*</i>
          <label for="city">Город</label><br>
          <input @blur="$v.formAddress.city.$touch()"
            :class="status($v.formAddress.city)"
            v-model.trim="formAddress.city"
            type="text" class="form-control" id="city" placeholder="Магнитогорск"><br>
          <span class="invalid-feedback" v-if="!$v.formAddress.city.required && $v.formAddress.city.$dirty">Не заполнено</span><br>
          <span class="invalid-feedback" v-if="!$v.formAddress.city.alphaSpace && $v.formAddress.city.$dirty">Запрещены цифры, и другие символы</span>
        </div>
        <!-- Улица -->
        <div class="form-group">
          <label for="street">Улица</label><br>
          <input 
            v-model.trim="formAddress.street"
            type="text" class="form-control" id="street"><br>
        </div>
        <!-- Дом -->
        <div class="form-group">
        <label for="house">Дом</label><br>
        <input @blur="$v.formAddress.house.$touch()"
          :class="status($v.formAddress.house)"
          v-model.trim="formAddress.house"
          type="text" class="form-control" id="house"><br>
        <span class="invalid-feedback" v-if="!$v.formAddress.house.house && $v.formAddress.house.$dirty">Запрещены символы, кроме цифр и /</span><br>
        </div>
      </div>
    </div>

    <div class="form-document-info">
      <div class="form-header">Документ</div>
      <div class="form-flex">
        <!-- Тип документа -->
        <div class="form-group">
          <i class="icon-required">*</i>
          <label for="type">Тип документа</label><br>
          <select @blur="$v.formDocument.type.$touch()"
            :class="status($v.formDocument.type)"
            v-model="formDocument.type"
            class="select-control" id="type" size="1">
              <option></option>
              <option>Паспорт</option>
              <option>Свидетельство о рождении</option>
              <option>Вод. удостоверение</option>
            </select>
            <br>
          <span class="invalid-feedback" v-if="!$v.formDocument.type.required && $v.formDocument.type.$dirty">Не выбран</span><br>
        </div>
        <!-- Серия -->
          <div class="form-group">
            <label for="seria">Серия</label><br>
            <input 
              v-model.trim="formDocument.seria"
              type="text" class="form-control" id="seria"><br>
        </div>
        <!-- Номер -->
        <div class="form-group">
          <label for="number">Номер</label><br>
          <input 
            v-model.trim="formDocument.number"
            type="text" class="form-control" id="number"><br>
        </div>
        <!-- Кем выдан -->
        <div class="form-group">
        <label for="organizationIssue">Кем выдан</label><br>
        <input
          v-model.trim="formDocument.organizationIssue"
          type="text" class="form-control" id="organizationIssue"><br>
        </div>
        <!-- Дата выдачи -->
        <div class="form-group">
          <i class="icon-required">*</i>
          <label for="dateIssue">Дата выдачи</label><br>
          <input @blur="$v.formDocument.dateIssue.$touch()"
            :class="status($v.formDocument.dateIssue)"
            v-model.trim="formDocument.dateIssue"
            type="text" class="form-control" id="dateIssue" placeholder="YYYY-MM-DD"><br>
          <span class="invalid-feedback" v-if="!$v.formDocument.dateIssue.required && $v.formDocument.dateIssue.$dirty">Не заполнено</span><br>
          <span class="invalid-feedback" v-if="!$v.formDocument.dateIssue.date && $v.formDocument.dateIssue.$dirty">Проверьте формат даты</span>
        </div>
      </div>
    </div>

    <p><i class="icon-required">*</i>Поле обязательное для заполнения.</p>
    <button class="btn" @click="onCreateClient">Зарегистрировать клиента</button>
    <div v-if="isShowMsg" class="result" :class="msgClass">{{ msg }}</div>
  </form>
</template>

<script>
import { required, helpers  } from 'vuelidate/lib/validators'

const alpha = helpers.regex('alpha', /^[a-zA-Zа-яёА-ЯЁ]*$/);
const alphaSpace = helpers.regex('alpha', /^[a-zA-Zа-яёА-ЯЁ\s]*$/);
const phone = helpers.regex('phone', /^7\d{10}$/);
const index = helpers.regex('index', /^\d{6}$/);
const house = helpers.regex('house', /^[1-9]+\/?\d+$|^\d*$/);
const date = helpers.regex('date', /(19|20)\d\d-((0[1-9]|1[012])-(0[1-9]|[12]\d)|(0[13-9]|1[012])-30|(0[13578]|1[02])-31)/);

export default {
  name: 'FormClient',
   data: () => ({
        isShowMsg: false,
        msg: '',
        msgClass:'',
        formReg: {
          name: '',
          surname: '',
          fatherName: '',
          birth: '',
          phone: '',
          gender: '',
          groupClient: [],
          doctor: '',
          isSms: false,
        },
        formAddress:{
          index: '',
          country: '',
          area: '',
          city: '',
          street: '',
          house: '',
        },
        formDocument: {
          type: '',
          seria: '',
          number: '',
          organizationIssue:'',
          dateIssue:'',
        }
  }),
  validations:{
    formReg:{
      name:{
        required,
        alpha,
      },
      surname:{
        required,
        alpha,        
      },
      birth:{
        required,
        date,   
      },
      phone:{
        required,
        phone,
      },
      groupClient: {
        required,
      }
    },
    formAddress:{
      index:{
        index,
      },
      country:{
        alphaSpace,
      },
      city:{
        required,
        alphaSpace,
      },
      house:{
        house,
      },
    },
    formDocument:{
      type:{
        required,
      },
      dateIssue:{
        required,
        date,
      }
    }
  },
  methods:{
    onCreateClient(event){
      event.preventDefault();
      this.$v.$touch();
      let valid  = this.checkValidForm();
      this.createResultMsg(valid);
      this.setFlagMessage();
    },
    checkValidForm(){
      if (this.$v.$invalid){
        return false;
      }
      else{
        return true;
      }
    },
    createResultMsg(valid){
      if(valid){
        this.msg = "Клиент успешно зарегистрирован!";
        this.msgClass = 'success';
      }
      else{
        this.msg = "Не удалось зарегистрировать клиента! Проверьте форму...";
        this.msgClass = 'failure';   
      }
    },
    setFlagMessage(){
      this.isShowMsg = true;
      setTimeout(() => {
        this.isShowMsg =false;
      }, 2000)
    },
    status(validation) {
       return {
         'error': validation.$error
       }
    },
  },
}
</script>

<style scoped>

.wrapper{
  max-width: 720px;
  box-shadow: 0 0 10px #000;
  border-radius: 10px;
  margin: 0 auto;
  padding: 20px 0px;
  background-image: linear-gradient(rgba(25,25,25,.0), rgba(25,25,25,.1));
}

.form-common-info,
.form-address-info,
.form-document-info{
  position: relative;
  margin: 30px 10px 0px;
  padding-top: 20px;
  border: 2px dotted #000;
  border-radius: 5px;
}

.form-flex{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.form-header{
  font-size: 16px;
  font-weight: bold;
  padding: 3px 10px;
  background-color: #fff;
  border: 2px dotted #000;
  border-radius: 5px;
  position: absolute;
  top: -13px;
  left: 17px;
}

.form-group{
  position: relative;
  text-align: left;
  margin: 15px;
}

label{
  font-size: 16px;
  font-weight: bold;
}

p{
  text-align: left;
  font-style: italic;
  font-size: 12px;
  margin: 10px ;
  padding: 0;
}
.btn{
  border-radius: 10px;
  border: 2px solid #000;
  background-color: #fff;
  font-size: 16px;
  font-weight: bold;
  padding: 10px 20px;
  box-shadow: 0 2px 5px #000;
}
.btn:hover{
  background-color: rgba(25,25,25,.2);
  color: #fff;
}
.btn:active{
  transform: scale(0.99);
}

.form-control{
  max-width: 100%;
  border-radius: 5px;
  border: 1px solid #000;
  margin-top:5px;
  padding: 11px 15px;
}

.select-control{
  width: 200px;
  border-radius: 5px;
  border: 1px solid #000;
  margin-top:5px;
  padding: 10px 15px;
}

.multyselect-control{
  width: 200px;
  border-radius: 5px;
  border: 1px solid #000;
  margin-top:5px;
  padding: 10px 15px 0px;
  overflow-y: auto;
}

.multyselect-control option{
  margin: 3px 0 ;
}

.checkBox-control{
  width: 14px;
  height: 14px;
  margin-right: 10px;
}
.icon-required{
  color: rgb(255, 100, 100);
  margin-right: 5px;
}

.error {
  background-color: #fdd;
  border: 1px solid red
}

.invalid-feedback{
  position: absolute;
  bottom: 0;
  color: red;
  font-size: 9px;
}

.result{
  margin-top: 10px;
  font-size: 14px;
  font-weight: bold;
}

.success{
  color: rgb(7, 112, 7);
}

.failure{
  color: rgb(255, 100, 100);
}
</style>