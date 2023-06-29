<template>
  <div class="wrapper">
    <div class="container">
      <h1>徵人留言板</h1>

      <label for="filterSkills">篩選技能：</label>
      <select name="filterSkills" id="filterSkills" v-model="filterSkill">
        <option value="">所有技能</option>
        <option value="主唱">主唱</option>
        <option value="吉他手">吉他手</option>
        <option value="貝斯手">貝斯手</option>
        <option value="鼓手">鼓手</option>
        <option value="鍵盤手">鍵盤手</option>
        <option value="其他樂器">其他樂器</option>
      </select>

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
            <img src="../assets/svgviewer-output.svg" alt="photo">
            <div class="memberInfo">
              <h2>找{{ item.findSkill }}</h2>
              <p>{{ item.userName }}</p>
              <p>{{ item.content }}</p>
            </div>
            <button class="exit-btn" @click="deleteCard(item)">Exit</button>
            <button class="edit-btn" @click="editCard(item)">Edit</button>
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
          </div>
        </li>
      </ul>
      
    </div>
  </div>
</template>

<script setup>
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

 
<style scoped>

.wrapper {
  color: #fff;
}

h1 {
  color: #fff;
  text-align: center;
  font-size: 30px;
}
  .wrapper {
    height: 800px;
    width: 100%;
    display: flex;
    justify-content: center;
    background-color: rgba(0, 0, 0, .8);
    background-image: url(../assets/glenn-van-de-wiel-DWHSc8o8K9Y-unsplash.jpg);
    background-size: cover;
    background-blend-mode: multiply;
    background-position: center center;
    
  }
  .container {
    width: 900px;
    height: 90px;
    margin: 20px auto;
  }

  .container h1 {
    color: #D1603D;
    font-weight: 600;
    font-size: 30px;
  }

  .items {
    text-align: center;
    background-color: #494747;
    color: #fff;
    border-radius: 5px;
    padding: 15px;
    display: flex;
    justify-content: space-around;
    align-items: center;
    margin: 15px auto;
    box-shadow: 0px 0px 5px rgba(255, 255, 255, 0.3)
  }

  .items h2 {
    color: #D1603D;
    font-weight: bold;
    font-size: 20px;
  }

  .items img {
    width: 50px;
    height: 50px;
    border-radius: 50px;
    border-top: 1px solid #414141;
  }

  .itemTitle {
    width: 100px;
  }

  .memberInfo {
    display: block;
  }
  

  .postBox {
    height: 80px;
    text-align: center;
    background-color: #D1603D;
    color: #fff;
    border-radius: 4px;
    padding: 15px;
    display: flex;
    justify-content: space-around;
    align-items: center;
    margin: 15px auto;
  }
  


</style>
