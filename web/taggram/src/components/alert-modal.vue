<template>
<div id="modal">
    <div class="icon">
        <img src="" alt="" srcset="">
    </div>
    <div class="message">
        {{text}}
    </div>
</div>
</template>

<script>
export default {
    props: ["text", "duration"],
    created() {
        var vm = this;

        setTimeout(function() {
            vm.$emit('close')
        }, this.duration * 1000)
    },
}
</script>

<style>
#modal {
    position: fixed;
    bottom: 25px;
    right: 25px;
    height: 65px;
    width: fit-content;
    background: rgb(198, 248, 98);
    border: 1px solid yellowgreen;
    border-radius: 3px;
    display: flex;
    align-items: center;
    padding: 0 25px;
}
</style>
