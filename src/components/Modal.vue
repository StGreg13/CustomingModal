<script setup lang="ts">
import { ref } from 'vue';

const dialog = ref<HTMLDialogElement>();

const props = defineProps({
  header: {
    type: String,
    default: "Название окна"
  },
  confirmText: {
    type: String,
    default: 'Confirm',
  },
  cancelText: {
    type: String,
    default: 'Cancel',
  },
  showConfirm: {
    type: Boolean,
    default: false,
  },
  showCancel: {
    type: Boolean,
    default: false,
  },
  classes: {
    type: String,
    default: '',
  },
});

const emit = defineEmits(['confirm', 'cancel']);

const cancel = () => {
  dialog.value?.close();
  emit('cancel');
};

const confirm = () => {
  dialog.value?.close();
  emit('confirm');
};

const visible = ref(false);

const showModal = () => {
  dialog.value?.showModal();
  visible.value = true;
};

defineExpose({
  show: showModal,
  close: (returnVal?: string): void => dialog.value?.close(returnVal),
  visible,
});
</script>

<template>
  <dialog
      ref="dialog"
      class="modal"
      @close="visible = false"
  >
    <form
        v-if="visible"
        method="dialog"
        :class="{
        'modal-box rounded-none p-4': true,
        [props.classes]: props.classes,
      }"
    >
      <div class="header">
        {{header}}
        <button class="close">
          <img src="../assets/close.svg" alt="close" >
        </button>
      </div>
      <div class="main">
        <slot />
      </div>

      <div class="footer" v-if="props.showConfirm || props.showCancel">
        <slot name="actionButtons">
          <button
              v-if="props.showCancel"
              value="false"
              class="btn cancel"
              @click.prevent="cancel"
          >
            {{ props.cancelText }}
          </button>
          <button
              v-if="props.showConfirm"
              value="true"
              class="btn accept"
              @click.prevent="confirm"
          >
            {{ props.confirmText }}
          </button>
        </slot>
      </div>
    </form>
  </dialog>
</template>

<style scoped>
  button {
    cursor: pointer;
  }
 .modal {
   top: 50%;
   left: 50%;
   width: 300px;
   padding: 0;
   transform: translate(-50%, -50%);
   border: 2px solid #0a2251;
   border-radius: 15px;
   text-align: center;
   background: #010b25;
 }
 .header {
   position: relative;
   background: #01143f;
   color: #579ee6;
   font-size: 14px;
   font-weight: 600;
   padding: 4px 12px;
   z-index: 10;
 }
 .close {
   position: absolute;
   top: 50%;
   right: 10px;
   transform: translate(0, -50%);
   background: inherit;
   border: none;
 }
 .close img {
   width: 14px;
 }
 .main {
   color: #8a9dbd;
   padding: 20px 10px;
 }
 .footer {
   position: relative;
   display: flex;
   flex-direction: row;
   justify-content: center;
   column-gap: 10px;
   background: #01143f;
   color: #579ee6;
   font-size: 18px;
   font-weight: 600;
   padding: 12px;
 }
 .btn {
   min-width: 50px;
   border-radius: 5px;
   padding: 6px 20px;
   color: #ffffff;
   font-weight: 500;
   letter-spacing: 1px;
   font-size: 12px;
   border: none;
 }
 .btn.cancel {
   background: #6d0617;
   box-shadow: inset 2px 2px 10px 5px #ff0000bd;
 }
 .btn.accept {
   background: #00720a;
   box-shadow: inset 2px 2px 10px 5px #01c512;
 }
</style>
