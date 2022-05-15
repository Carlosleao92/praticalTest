<template>
    <form v-on:submit.prevent>
        <input
            v-model="innerValue"
            :placeholder="placeholder"
            :name="name"
            style="number"
            class="phoneInput"
            @input="onInput($event.currentTarget.value)"
			@keyup.enter="onSubmit($event)"
        />
    </form>
</template>

<script>
export default {
    data() {
        return {
            innerValue: this.value,
			isValid: true
        };
    },
    props: {
        placeholder: {
            type: String,
            default: "",
        },
        name: {
            type: String,
            default: "",
        },
        value: {
            type: [Number, String],
            default: null,
        }
    },
    watch: {
        value(newValue) {
            this.innerValue = newValue;
        }
    },
    methods: {
        onInput() {
			this.validate()
			if (!this.isValid) {
				this.innerValue = this.innerValue.slice(0, -1)
			}
			this.$emit('input', this.innerValue)

			
        },
        onSubmit(e) {
            if (this.isValid) {
				this.$emit('enter', e.target.value)
			}
        },
		validate () {
			const regex =  /^[0-9 +]+$/
			this.isValid = regex.test(this.innerValue)
			return this.isValid
		}
    },
};
</script>

<style scoped>
.phoneInput {
    height: 2rem;
    background: #2c3e50;
    border: 0.5rem #42b983 solid;
	border-radius: 2rem;
	margin: 2rem;
	color: white;
	padding: 0px 2rem;
	text-align: center;
	-moz-appearance: textfield;

}
::placeholder {
	color: #42b983;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

</style>