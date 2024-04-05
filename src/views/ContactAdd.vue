<template>
    <div class="page">
        <h4>Thêm mới Liên hệ</h4>
        <form @submit.prevent="addContact">
            <div class="form-group">
                <label for="name">Tên:</label>
                <input type="text" class="form-control" id="name" v-model="newContact.name" required>
            </div>
            <div class="form-group">
                <label for="email">Email:</label>
                <input type="email" class="form-control" id="email" v-model="newContact.email" required>
            </div>
            <div class="form-group">
                <label for="address">Địa chỉ:</label>
                <input type="text" class="form-control" id="address" v-model="newContact.address" required>
            </div>
            <div class="form-group">
                <label for="phone">Số điện thoại:</label>
                <input type="tel" class="form-control" id="phone" v-model="newContact.phone" required>
            </div>
            <button type="submit" class="btn btn-primary">Thêm Liên hệ</button>
        </form>
    </div>
</template>

<script>
import ContactService from "@/services/contact.service";

export default {
    data() {
        return {
            newContact: {
                name: '',
                email: '',
                address: '',
                phone: ''
            }
        };
    },
    methods: {
        async addContact() {
            try {
                await ContactService.create(this.newContact); // Sử dụng ContactService để thêm liên hệ mới
                // Sau khi thêm thành công, chuyển hướng người dùng về trang danh bạ
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.error("Error adding contact:", error);
                // Xử lý lỗi nếu cần
            }
        }
    },
};
</script>

<style scoped>
.page {
    max-width: 500px;
    margin: 0 auto;
}
</style>
