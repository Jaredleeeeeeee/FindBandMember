<template>
  <div class="wrapper">
    <h1>徵人留言板</h1>

    <div class="container">
      <!-- 篩選樂器選項 -->
      <label for="filterSkills">篩選樂器：</label>
      <select name="filterSkills" id="filterSkills" v-model="filterSkill">
        <option value="">所有技能</option>
        <option value="主唱">主唱</option>
        <option value="吉他手">吉他手</option>
        <option value="貝斯手">貝斯手</option>
        <option value="鼓手">鼓手</option>
        <option value="鍵盤手">鍵盤手</option>
        <option value="其他樂器">其他樂器</option>
      </select>
    </div>

    <div class="postBox">
      <form @submit.prevent="addCard">
        <label for="skills">我要找：</label>
        <select name="skills" id="skills" v-model="newFindSkill">
          <option value="主唱">主唱</option>
          <option value="吉他手">吉他手</option>
          <option value="貝斯手">貝斯手</option>
          <option value="鼓手">鼓手</option>
          <option value="鍵盤手">鍵盤手</option>
          <option value="其他樂器">其他樂器</option>
        </select>
        <label for="name">姓名: </label><input type="text" v-model="newUserName" required>
        <label for="postInput">發文內容: </label><input type="text" id="postInput" v-model="newContent" required>
        <button type="submit">Submit</button>
      </form>
    </div>

    <ul class="itemsList">
      <li v-for="item in filteredList" :key="item.id">
        <div class="items">
          <div class="avatar_container">
            <img src="../assets/user.png" alt="photo">
            <h3>{{ item.userName }}</h3>
          </div>
          <div class="memberInfo">
            <h2>找：{{ item.findSkill }}</h2>
            <p>{{ item.content }}</p>
          </div>
          <div class="actions">
            <button class="exit-btn" @click="deleteCard(item)">EXIT</button>
            <button class="edit-btn" @click="editCard(item)">EDIT</button>
          </div>
          <Teleport to="body">
            <EditCard :show="editingItem === item" @close="editingItem = null">
              <template #body>
                <div class="edit_card">
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
              </template>
            </EditCard>
          </Teleport>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import EditCard from './EditCard.vue';
import { ref, computed } from 'vue';

let id = 0;

const newFindSkill = ref('主唱');
const newUserName = ref(null);
const newContent = ref(null);
const editingItem = ref(null);
const filterSkill = ref(null);

const list = ref([
  { id: id++, findSkill: '主唱', userName: '王小明', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Natus asperiores delectus voluptatem minus expedita, repellat ut provident vero non mollitia!', isFindMember: false },
  { id: id++, findSkill: '鼓手', userName: '孫小美', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Natus asperiores delectus voluptatem minus expedita, repellat ut provident vero non mollitia!', isFindMember: false },
  { id: id++, findSkill: '鍵盤手', userName: '李炳輝', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Natus asperiores delectus voluptatem minus expedita, repellat ut provident vero non mollitia!', isFindMember: false }
]);

const addCard = () => {
  const newItem = {
    findSkill: newFindSkill.value,
    userName: newUserName.value,
    content: newContent.value
  };
  list.value.push(newItem);
  newFindSkill.value = '主唱';
  newUserName.value = null;
  newContent.value = null;
};

const deleteCard = (item) => {
  list.value = list.value.filter((t) => t !== item);
};

const editCard = (item) => {
  editingItem.value = item;
};

const saveEdit = (item) => {
  editingItem.value = null;
};

const filteredList = computed(() => {
  if (!filterSkill.value) {
    return list.value;
  } else {
    return list.value.filter((item) => {
      return item.findSkill === filterSkill.value;
    });
  }
});
</script>


<style lang="scss" scoped>
$primary-color: #D1603D;
$secondary-color: #E8A98D;
$background-color: #F7F5F5;

.wrapper {
  height: 960px;
  padding: 20px;
  display: flex;
  flex-direction: column;
  background-color: rgba(0, 0, 0, .8);
  background-image: url(../assets/glenn-van-de-wiel-DWHSc8o8K9Y-unsplash.jpg);
  background-size: cover;
  background-blend-mode: multiply;
  background-position: center center;
  background-attachment: fixed;

  h1 {
    color: $primary-color;
    text-align: center;
    font-size: 30px;
    font-weight: bold;
  }

  ;


  .container {
    margin: 20px auto;
    display: flex;
    align-items: center;
    justify-content: center;
    font-style: 18px;
    color: $secondary-color;

    label {
      margin-right: 10px;
    }

    ;

    select {
      padding: 5px;
      border: 1px solid $secondary-color;
      border-radius: 4px;
    }
  }

  .postBox {
    margin-bottom: 20px;

    form {
      display: flex;
      flex-direction: column;

      label {
        margin-bottom: 10px;
        font-size: 18px;
        color: $primary-color
      }

      ;

      select,
      input[type="text"] {
        padding: 10px;
        border: none;
        border-radius: 4px;
        background-color: $background-color;
        border: 1px solid $secondary-color;
        margin-bottom: 10px;
        font-size: 16px;
      }

      button[type="submit"] {
        padding: 10px 20px;
        background-color: $primary-color;
        color: #fff;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-size: 16px;
        transition: background-color 0.3s ease;

        &:hover {
          background-color: darken($primary-color, 10%);
        }
      }
    }
  }
}

.itemsList {
  list-style-type: none;
  padding: 0;
  min-height: 400px;
  overflow-y: scroll;
}


.items {
  background: #494747;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, .1);
  padding: 20px;
  margin-bottom: 20px;
  display: flex;
  align-items: center;


  img {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    margin-right: 10px;
  }

  ;

  .content {
    flex-grow: 1;
  }

  h3 {
    margin: 0;
    color: $primary-color;
    font-size: 18px;
  }

  ;

  .memberInfo {
    margin: 0;
    width: 800px;

    h2 {
      color: $secondary-color;
      font-weight: bold;
      font-size: 20px;
      margin-top: 5px;
      text-align: center;
    }

    p {
      color: #fff;
      font-size: 16px;
      margin: 5px 0;
      text-indent: 1em;
    }
  }

  .actions {
    display: flex;
    align-items: center;
    justify-content: space-around;
    flex-wrap: wrap;

    .exit-btn,
    .edit-btn {
      padding: 8px 16px;
      border-color: #f44336;
      color: #494747;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      margin: 10px;
      font-size: 14px;
      transition: background-color 0.3s ease;

      &:hover {
        background-color: darken(#f44336, 10%);
      }
    }
  }

  .edit_card {
    margin-top: 10px;
    padding: 10px;
    border-color: $background-color;

    form {
      display: flex;
      flex-direction: column;

      label {
        margin-bottom: 6px;
        font-size: 16px;
        color: $primary-color;
      }

      select,
      input[type="text"] {
        padding: 10px;
        border: none;
        border-radius: 4px;
        background-color: $background-color;
        border: 1px solid $secondary-color;
        margin-bottom: 10px;
        font-size: 14px;
      }

      button[type="submit"] {
        padding: 10px 20px;
        border-color: $primary-color;
        color: #494747;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-size: 14px;
        transition: background-color 0.3s ease;

        &:hover {
          background-color: darken($primary-color, 10%);
        }
      }
    }
  }
}

@media (min-width: 768px) {

  .postBox {
    margin: 0 auto;
    width: 60%;
  }

  .itemsList {
    margin: 0 auto;
    width: 80%;
  }
}</style>
