<template>
    <section class="interactive-card">
        <div class="cards">
            <CardBack :cvc="formData.cvc"/>
            <CardFront :cardholder-name="formData.cardholderName" :card-number="formData.cardNumber" :month="formData.month" :year="formData.year"/>
        </div>
        <div class="form-side">
            <form>
                <div class="form-group">
                    <label for="cardholder-name">Cardholder name</label>
                    <input type="text" id="cardholder-name" v-model="formData.cardholderName" placeholder="e.g. Jane Appleseed">
                    <p v-if="$v.cardholderName.$error" class="error-message">
                        {{$v.cardholderName.$errors[0].$message}}
                    </p>
                </div>
                
                <div class="form-group">
                    <label for="card-number">Card number</label>
                    <input type="text" id="card-number" v-model="formData.cardNumber" placeholder="e.g. 1234 5678 9123 0000">
                    <p v-if="$v.cardNumber.$error" class="error-message">
                        {{$v.cardNumber.$errors[0].$message}}
                    </p>
                </div>

                <div class="form-group">
                    <label>Exp. date (mm/yy)</label>
                    <input type="text" v-model.number="formData.month" placeholder="MM">
                    <input type="text" v-model.number="formData.year" placeholder="YY">
                    <p class="error-message">
                        <span v-if="$v.month.$error">{{$v.month.$errors[0].$message}}</span>
                        <span v-if="$v.year.$error">{{$v.year.$errors[0].$message}}</span>
                    </p>
                </div>
                
                <div class="form-group">
                    <label for="cvc">CVC</label>
                    <input type="text" id="cvc" v-model="formData.cvc" placeholder="e.g. 123" maxlength="3">
                    <p v-if="$v.cvc.$error" class="error-message">
                        {{$v.cvc.$errors[0].$message}}
                    </p>
                </div> 
                <ConfirmButton @submit="submitForm"/>
            </form>
        </div>
    </section>

</template>

<script setup>
    import { useVuelidate } from '@vuelidate/core'
    import { required, integer, minLength, between, helpers } from '@vuelidate/validators'
    import { reactive, computed } from 'vue';
    import CardFront from './CardFront.vue';
    import CardBack from './CardBack.vue';
    import ConfirmButton from './ConfirmButton.vue'

    const currentYear = new Date().getFullYear()

    const cardNumberLength = (value)=>{
        return value.length === 16;
    }

    const lettersOnly = (value)=>{
        const pattern = /^[A-Za-z\s]*$/
        return pattern.test(value)
    }

    const formData = reactive({
        cardholderName: '',
        cardNumber: '',
        month: '',
        year: '',
        cvc: ''
    })

    const rules = computed(()=>{
        return {
            cardholderName: {
                required: helpers.withMessage('Cardholder name is required', required),
                minLength: minLength(4),
                lettersOnly: helpers.withMessage('The name should contain only letters', lettersOnly)
            },
            cardNumber: { 
                required: helpers.withMessage('Card number is required', required),
                integer,
                cardNumberLength: helpers.withMessage('The card must have 16 digits', cardNumberLength) 
            },
            month: { 
                required: helpers.withMessage('Month is required',required),
                integer,
                between: between(1,12)
            },
            year: {
            required: helpers.withMessage('Year is required', required),
            integer,
            between: between(currentYear, currentYear+20)
            },
            cvc: {
                required: helpers.withMessage('CVC is required', required),
                integer,
                minLength: minLength(3)
            }
        }
    })

    const $v = useVuelidate(rules, formData)

    const submitForm = async ()=>{
        const result = await $v.value.$validate();
        if(result){
            console.log('Form is ok')
        }else{
            console.log('Form is not valid :(')
        }
    }
</script>   

<style lang="scss" scoped>
    .error-message{
        color: red;
    }
</style>