
<template>
    <Modal
        v-model="FEHPVBmodal"
        title="title"
        ok-text="ok"
        cancel-text="cancel"
        footer-hide
        @on-ok=""
        @on-cancel=""
        :closable="false"
    >
        <div>
            content
            <div slot="footer">
                <Button @click="" type="primary">确认</Button>
                <Button @click="">取消</Button>
            </div>
        </div>
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
