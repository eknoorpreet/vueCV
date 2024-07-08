<template>
  <CustomButton
    btn-type="primary"
    @click="exportPDF"
    style="margin-bottom: 10px"
  >
    Export resume as PDF
  </CustomButton>
</template>

<script>
import CustomButton from './CustomButton.vue';
export default {
  components: {
    CustomButton,
  },
  props: {
    resumeFormat: {
      type: String,
    },
  },
  methods: {
    exportPDF() {
      const unit = this.resumeFormat == 'a4' ? 'mm' : 'in';
      const pdfConfig = {
        margin: 0,
        filename: 'resume',
        jsPDF: {
          unit,
          format: this.resumeFormat,
          orientation: 'portrait',
        },
      };
      html2pdf().set(pdfConfig).from(resume).save();
    },
  },
};
</script>

<style></style>
