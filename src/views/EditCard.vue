
<template>
    <Transition name="modal">
        <div v-if="show" class="modal-mask">
            <div class="modal-container">
                <div class="modal-body">
                    <slot name="body">
                        <div class="edit_card" v-if="editingItem === item">
                            <form @submit.prevent="saveEdit(item)">
                                <label for="editFindSkill">找:</label>
                                <select name="editFindSkill" id="editFindSkill" v-model="item.findSkill">
                                    <option value="主唱">主唱</option>
                                    <option value="吉他手">吉他手</option>
                                    <option value="貝斯手">貝斯手</option>
                                    <option value="鼓手">鼓手</option>
                                    <option value="鍵盤手">鍵盤手</option>
                                    <option value="其他樂器">其他樂器</option>
                                </select><br>
                                <label for="editUserName">姓名:</label>
                                <input type="text" name="editUserName" id="editUserName" v-model="item.userName">
                                <label for="editContent">內容:</label>
                                <input type="text" name="editContent" id="editContent" v-model="item.content"><br>
                                <button type="submit">Save</button>
                            </form>
                        </div>
                    </slot>
                </div>
            </div>
        </div>
    </Transition>
</template>
  
<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    show: Boolean
});
</script>
  
<style>
.modal-mask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    transition: opacity 0.3s ease;
}

.modal-container {
    width: 350px;
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
    padding: 20px;
}

.modal-body {
    margin: 20px 0;
}

.edit_card form {
    display: flex;
    flex-direction: column;
}

.edit_card label {
    margin-bottom: 5px;
}

.edit_card input,
.edit_card select {
    padding: 5px;
    margin-bottom: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    height: 40px;
}

.edit_card button {
    padding: 5px 10px;
    background-color: #b5b5b5;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    height: 50px;
    font-size: x-large;
}

.edit_card button:hover {
    background-color: #D1603D;
}
</style>
  