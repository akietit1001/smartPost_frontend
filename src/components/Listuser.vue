<template>
    <div class="wrapper">
        <div class="list-title">管理者一覧</div>
        <Button class="btn-add" :primary="ref(true).value" :text="'+ 管理者の追加'" />
        <div>
            <el-tabs v-model="activeName" class="demo-tabs">
                <SearchInput :placeholder="'テキストを検索'" :on-change="handleFillUser"/>
                <el-tab-pane label="登録済み" name="first"><TableVue :data="data" /></el-tab-pane> 
                <el-tab-pane label="招待中" name="second"><TableVue :data="data"  /></el-tab-pane>
            </el-tabs>
        </div>
        <Pagination />
    </div>
</template>

<script setup lang="ts">
import { ref, onBeforeMount } from 'vue';
import { adminApi } from "@/apis/adminApi";
import Button from './Button.vue'
import SearchInput from './SearchInput.vue';
import TableVue from './Table.vue';
import Pagination from './Pagination.vue'
const value = ref('');
const data = ref([]);
const activeName = ref('first')

onBeforeMount(async ()=>{
  const response = await adminApi.getAdmin('/getall');
  data.value = response.data;
  console.log(data.value)
})

const handleFillUser = (e) => {
   value.value = e.target.value
   console.log(value.value)
   console.log(data.value.find(user => {
    user['email'] === value.value;
   }))
}

</script>

<style>

.list-title{
    margin-top: 20px;
    font-size: 20px;
}
.btn-add{
    margin: 20px 0;
}
.icon-plus{
    margin-right: 5px;
}
.demo-tabs > .el-tabs__content {
  color: #6b778c;
  font-size: 16px;
}
.el-tabs__item.is-top:hover{
    color: #35CFAA;
}
.el-tabs__item.is-active{
    
    color: #222 !important;
}
.el-tabs__active-bar.is-top{
    height: 4px;
    background-color: #35CFAA;
}
</style>