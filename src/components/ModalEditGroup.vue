<template>
  <div>
    <Button :text="t('admin_info.change')" @click="modalGroupVisible = true" :primary="ref(true).value" />

    <el-dialog v-model="modalGroupVisible" :title="title">
      <div class="modal-edit-name-body">
        <InputText :label="t('modalEditGroup.group')" type="text" :placeholder="t('modalEditGroup.enterGroup')" />
      </div>
      <template #footer>
        <span class="dialog-footer">
          <Button :text="t('admin_info.change')" :primary="ref(true).value" @click="modalGroupVisible = false"/>
        </span>
      </template>
    </el-dialog>
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue';
import { useI18n } from 'vue-i18n';
import Button from './Button.vue';
import InputText from './InputText.vue';

const { t } = useI18n()
const modalGroupVisible = ref(false)
defineProps<{
  title: string
}>()
</script>

<style>
.modal.fade.show {
  display: flex !important;
  align-items: center;
}

.wrapper-model-body{
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
}
.modal .modal-content{
  width: 460px;
  border-radius: 0;
}
.modal .modal-footer{
  justify-content: center;
}
</style>