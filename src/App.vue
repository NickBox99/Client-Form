<template>
  <form id="clientForm" @submit.prevent = "submitForm">
		<h1 class="title">Форма создания Клиента</h1>


		<h4 class="titleForm">Личные данные:</h4>
		<div class="row">
			<div class="col-50">
				<div class="box box-column">
					<label for="name">Имя*:</label>
					<input type="text" id="name"
           v-model.trim="name" 
          :class="{invalid: ($v.name.$dirty && !$v.name.required) || ($v.name.$dirty && !$v.name.validFormat)}">
				</div>
			</div>

			<div class="col-50">
				<div class="box box-column">
					<label for="surname">Фамилия*:</label>
					<input type="text" id="surname"
           v-model.trim="surname" 
          :class="{invalid: ($v.surname.$dirty && !$v.surname.required) || ($v.surname.$dirty && !$v.surname.validFormat)}">
				</div>
			</div>
		</div>

		<div class="box box-column">
			<label for="lastName">Отчество:</label>
			<input type="text" id="lastName" v-model.trim="lastName" >
		</div>

		<div class="box box-row">
			<label for="dateOfBirth">Дата рождения*: </label>
			<input type="date" id="dateOfBirth" min="1900-01-01" max="2020-12-31"
        v-model.trim="dateOfBirth"
        :class="{invalid: $v.dateOfBirth.$dirty && !$v.dateOfBirth.required}">
		</div>

		<div class="box box-row">
			<label for="phone">Номер телефона*:</label>
			<input type="phone" id="phone"
        v-model.trim="phone"
        :class="{invalid: ($v.phone.$dirty && !$v.phone.required) || ($v.phone.$dirty && !$v.phone.validFormat) || ($v.phone.$dirty && !$v.phone.maxLength)}">
		</div>

		<div class="box box-row">
			<label for="sexOfAPerson">Пол:</label>
			<input type="text" id="sexOfAPerson"
        v-model.trim="sexOfAPerson">
		</div>

		<div class="box box-row">
			<label for="groupClient">Группа клиентов*:</label>
			<select name="groupClient" id="groupClient" multiple
        v-model.trim="groupClient" 
        :class="{invalid: $v.groupClient.$dirty && !$v.groupClient.required}">
				<option value="VIP">VIP</option>
				<option value="Проблемные">Проблемные</option>
				<option value="ОМС">ОМС</option>
			</select>
		</div>

		<div class="box box-row">
			<label for="doctor">Лечащий врач:</label>
			<select name="doctor" id="doctor" v-model.trim="doctor">
				<option value="Иванов">Иванов</option>
				<option value="Захаров">Захаров</option>
				<option value="Чернышева">Чернышева</option>
			</select>
		</div>

		<input type="checkbox" class="form-checkbox" id="form-checkbox" name="form-checkbox" value="yes" v-model.trim="formCheckbox">
		<label for="form-checkbox">Не отправлять СМС</label>



		<h4 class="titleForm">Адрес:</h4>
		<div class="row">
			<div class="col-50">
				<div class="box box-column">
					<label for="country">Страна:</label>
					<input type="text" id="country" v-model.trim="country">
				</div>
			</div>

			<div class="col-50">
				<div class="box box-column">
					<label for="city">Город*:</label>
					<input type="text" id="city" 
            v-model.trim="city"
            :class="{invalid: ($v.city.$dirty && !$v.city.required) || ($v.city.$dirty && !$v.city.validFormat)}">
				</div>
			</div>
		</div>

		<div class="row">
			<div class="col-50">
				<div class="box box-column">
					<label for="region">Область:</label>
					<input type="text" id="region" v-model.trim="region">
				</div>
			</div>

			<div class="col-50">
				<div class="box box-column">
					<label for="street">Улица:</label>
					<input type="text" id="street" v-model.trim="street">
				</div>
			</div>
		</div>

		<div class="row">
			<div class="col-50">
				<div class="box box-column">
					<label for="house">Дом:</label>
					<input type="text" id="house" v-model.trim="house">
				</div>
			</div>

			<div class="col-50">
				<div class="box box-column">
					<label for="index">Индекс:</label>
					<input type="text" id="index" v-model.trim="index">
				</div>
			</div>
		</div>


		<h4 class="titleForm">Паспортные данные:</h4>
		<div class="box box-row">
			<label for="typeDocument">Тип документа*:</label>
			<select name="typeDocument" id="typeDocument" 
        v-model.trim="typeDocument"
        :class="{invalid: $v.typeDocument.$dirty && !$v.typeDocument.required}"
        >
				<option value="Паспорт">Паспорт</option>
				<option value="Свидетельство о рождении">Свидетельство о рождении</option>
				<option value="Вод. удостоверение">Вод. удостоверение</option>
			</select>
		</div>

		<div class="row">
			<div class="col-50">
				<div class="box box-column">
					<label for="seriaDocument">Серия:</label>
					<input type="text" id="seriaDocument" v-model.trim="seriaDocument">
				</div>
			</div>

			<div class="col-50">
				<div class="box box-column">
					<label for="numberDocument">Номер:</label>
					<input type="text" id="numberDocument" v-model.trim="numberDocument">
				</div>
			</div>
		</div>

		<div class="box box-column">
			<label for="issued">Кем выдан:</label>
			<input type="text" id="issued" v-model.trim="issued">
		</div>

		<div class="box box-row">
			<label for="dateIssued">Дата выдачи*:</label>
			<input type="date" id="dateIssued" min="1900-01-01" max="2020-12-31" 
        v-model.trim="dateIssued"
        :class="{invalid: $v.dateIssued.$dirty && !$v.dateIssued.required}">
		</div>

		<button type="submit" id="sumbit">Отправить данные</button>
	</form>
</template>

<script>

import {required, maxLength} from 'vuelidate/lib/validators'

export default {
  name: 'clientForm',
  components: {
  },
  data: () => ({
    name: '',
    surname: '',
    lastName: '',
    dateOfBirth: '',
    phone: '',
    sexOfAPerson: '',
    groupClient: [],
    doctor: '',
    formCheckbox: '',
    country: '',
    city: '',
    region: '',
    street: '',
    house: '',
    index: '',
    typeDocument: '',
    seriaDocument: '',
    numberDocument: '',
    issued: '',
    dateIssued: '',

  }),
  validations:{
    name: {
      required,
      validFormat: val => !/[0-9]/.test(val),
    },
    surname: {
      required,
      validFormat: val => !/[0-9]/.test(val)
      },
    dateOfBirth: {required},
    phone: {
      required,
      maxLength: maxLength(12),
      validFormat: val => /\+?[78]([-()]*\d){10}/.test(val)
    },
    groupClient: {
      required,
    },
    typeDocument: {
      required,
    },
    city: {
      required,
      validFormat: val => !/[0-9]/.test(val),
    },
    dateIssued: {required},
  },
  methods: {
    submitForm(){
      if(this.$v.$invalid){
        alert('Необходимо заполнить все обязательные поля');
        this.$v.$touch()
        return
      }

      const formData = {
        name: this.name,
        surname: this.surname,
        lastName: this.lastName,
        dateOfBirth: this.dateOfBirth,
        phone: this.phone,
        sexOfAPerson: this.sexOfAPerson,
        groupClient: this.groupClient,
        doctor: this.doctor,
        formCheckbox: (this.formCheckbox)? true : false,
        country: this.country,
        city: this.city,
        region: this.region,
        street: this.street,
        house: this.house,
        index: this.index,
        typeDocument: this.typeDocument,
        seriaDocument: this.seriaDocument,
        numberDocument: this.numberDocument,
        issued: this.issued,
        dateIssued: this.dateIssued,
      }


      console.log('Новый созданный клиент: ', formData);
    
      alert("Клиент успешно создан");
    }
  }
}
</script>

<style>
*, *:after, *:before {
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
}

body {
  margin: 30px;
  font-size: 17px;
  font-family: 'Roboto', sans-serif;
}

.title {
  position: absolute;
  top: -1.1rem;
  right: 1rem;
  margin: 0;
  font-family: serif;
  color: #FFA957;
  font-size: 1.6rem;
  background-color: #fff;
}

.titleForm {
  margin-bottom: 0.6rem;
  color: #4b65b6;
}

#clientForm {
  position: relative;
  min-width: 250px;
  max-width: 500px;
  padding: 1rem;
  border: 1px solid #04A1A1;
}

.box {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -ms-flex-wrap: wrap;
      flex-wrap: wrap;
  margin-bottom: 1rem;
}

.box-column {
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}

.box-row {
  -webkit-box-align: center;
      -ms-flex-align: center;
          align-items: center;
}

.row {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -ms-flex-wrap: wrap;
      flex-wrap: wrap;
  -webkit-box-pack: justify;
      -ms-flex-pack: justify;
          justify-content: space-between;
}

.col-50 {
  -ms-flex-preferred-size: 46%;
      flex-basis: 46%;
}

#sumbit {
  display: block;
  margin-left: auto;
  padding: 1rem 0;
  width: 46%;
  color: #fff;
  border: none;
  background-color: #4b65b6;
}

.invalid{
  border: 1px solid red;
}

@media screen and (max-width: 470px) {
  .title {
    top: -0.8rem;
    font-size: 1.2rem;
  }
  .col-50 {
    -ms-flex-preferred-size: 100%;
        flex-basis: 100%;
  }
  #sumbit {
    width: 100%;
  }
}

@media screen and (max-width: 300px) {
  .title {
    position: unset;
    display: block;
    font-size: 1rem;
    margin: 0 auto;
  }
}
</style>
