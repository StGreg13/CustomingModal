<script setup lang="ts">
import { ref } from 'vue';
import Modal from './components/Modal.vue';
import Textonly from "@/components/Textonly.vue";
import Withcontent from "@/components/Withcontent.vue";

const modal = ref<InstanceType<typeof Modal>>();
const showModal = () => modal.value?.show();
</script>

<template>
  <button class="btn btn-primary" @click="showModal">Show Modal</button>
  <Modal
      ref="modal"
      header="Ошибка входа"
      confirmText="Перезагрузить"
      showConfirm=true
  >
    <Withcontent
        img="error"
        title-color=""
        light="radial-gradient(circle, rgba(255, 0, 0, 0.75) 0%, rgba(255, 0, 0, 0.35) 25%, rgba(0,0,0,0) 60%)"
        title-text="Повторный вход"
        text="Вы вошли в игру на другом устройстве или в другом окне"
    />
  </Modal>

</template>