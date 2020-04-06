<template>
    <Modal
        v-model="FEHPVBmodal"
        title="title"
        @on-ok=""
        @on-cancel=""
        :closable="false"
      >
        <div>content</div>
    </Modal>
</template>

<script>
export default {
  data(){
    return {
        FEHPVBmodal: false
    }
  }
}
</script>
