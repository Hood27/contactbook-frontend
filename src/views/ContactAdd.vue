<template>
  <div v-if="!contact" class="page">
    <h4>Thêm Liên hệ mới</h4>
    <ContactForm :contact="{}" @submit:contact="createContact" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
  components: {
    ContactForm,
  },
  data() {
    return {
      contact: null,
      message: "",
    };
  },
  methods: {
    async createContact(data) {
      try {
        const newContact = await ContactService.create(data);
        this.message = "Liên hệ mới đã được tạo thành công.";
        this.$router.push({ name: "contact.edit", params: { id: newContact._id } });
      } catch (error) {
        console.log(error);
        this.message = "Đã xảy ra lỗi khi tạo liên hệ mới.";
      }
    },
  },
};
</script>
