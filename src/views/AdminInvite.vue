<template>
  <div class="wrapper__admin-invite">
    <div class="inner__admin-invite">
      <NavSub :title="t('admin_invite.addAdmin')" />
      <div class="title__admin-invite">{{ t('admin_invite.addAdmin') }}</div>
      <Button class="btn__admin-invite" :text="t('listUser.addAdmin')" :primary="ref(true).value" @click="handleAddFormData"/>
    </div>
    <TableAdminInvite :children="children" @remove-form-data="handleRemoveFormData"/>
  </div>
</template>

<script setup lang="ts">
import {ref} from 'vue'
import NavSub from '@/components/NavSub.vue';
import Button from '@/components/Button.vue';
import TableAdminInvite from '@/components/TableAdminInvite.vue';
import { useI18n } from 'vue-i18n';

const { t } = useI18n()

let i = 0;
let n = 0;

const children = ref<{
  id: number
  child: number
}[]>([])

const handleAddFormData = () => {
  children.value.push({
    id: i++,
    child: n++
  })
}

const handleRemoveFormData = (id: number) => {
  children.value.splice(id, 1);
}


</script>

<style scoped>
.wrapper__admin-invite{
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.title__admin-invite{
  font-size: 20px;
}

.btn__admin-invite{
  margin: 15px 0;
}
</style>