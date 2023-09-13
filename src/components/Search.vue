<template>
    <form class="input-group mb-3">
        <div class="input-group-text">
            <svg viewBox="0 0 16 16" width="1em" height="1em" focusable="false" role="img" aria-label="search" xmlns="http://www.w3.org/2000/svg" fill="currentColor" class="bi-search b-icon bi"><g><path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"></path></g>
            </svg>
        </div>
        <input
            type="text"
            class="form-control"
            placeholder="Имя пользователя получателя"
            aria-label="Имя пользователя получателя"
            aria-describedby="button-addon2"
            v-model="searchValue"
        >
    </form>
</template>

<script>
export default {
    emits: ['value'],
    props: {
        value:String,
    },
    data() {
        return {
            searchValue: '',
        }
    },
    created(){
        this.searchValue = this.value
    } ,
    watch: {
        searchValue() {
            this.$emit('search', this.searchValue)
        }
    },
}
</script>

<style scoped>

</style>
