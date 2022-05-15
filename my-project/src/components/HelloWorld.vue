<template>
    <div v-if="!mock" class="hello">
        <img alt="Vue logo" src="../assets/logo.png" />
        <h1>Welcome</h1>
        <div>Hello this is Phone Input</div>
        <phone-input
            :value="value"
            :placeholder="'Click here'"
            @input="update($event)"
            @enter="handleSubmit($event)"
        />
        <h3>Please insert your phone</h3>
        <div v-if="list.length">
            <div v-for="entry in list" :key="entry">
                <p>{{ entry }}</p>
            </div>
        </div>
    </div>
</template>

<script>
import PhoneInput from "@/components/PhoneInput.vue";

export default {
    name: "HelloWorld",
    data() {
        return {
            value: null,
            list: [],
        };
    },
    props: {
        msg: String,
    },
    components: {
        PhoneInput,
    },
    methods: {
        update(e) {
            this.value = e;
        },
        handleSubmit() {
            this.list.push(this.value);
            this.value = null;
        },
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    margin: 10px 0 0;
}
ul {
    list-style-type: none;
    padding: 0;
}
li {
    display: inline-block;
    margin: 0 10px;
}
a {
    color: #42b983;
}
</style>
