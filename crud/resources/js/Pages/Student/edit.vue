<template>
    <AppLayout>
        <div class="row justify-content-center">
            <div class="col-6">
                <div class="card mt-3">
                    <div class="card-header">
                        <div class="d-flex justify-content-between">
                            <h3>Student Edit</h3>
                            <Link :href="route('students.index')" class="btn btn-primary">Back</Link>
                        </div>
                    </div>
                    <div class="card-body">
                        <form @submit.prevent="updateData">
                            <div class="mb-3">
                                <label for="name" class="form-label">Name</label>
                                <input v-model="form.name" type="text" class="form-control" :class="{'is-invalid':form.errors.name}" id="name">
                                <span v-if="form.errors.name" class="invalid-feedback">{{ form.errors.name }}</span>
                            </div>
                            <div class="mb-3">
                                <label for="email" class="form-label">Email address</label>
                                <input v-model="form.email" type="email" class="form-control" :class="{'is-invalid':form.errors.email}" id="email">
                                <span v-if="form.errors.email" class="invalid-feedback">{{ form.errors.email }}</span>
                            </div>
                            <div class="mb-3">
                                <label for="age" class="form-label">age</label>
                                <input v-model="form.age" type="integer" class="form-control" :class="{'is-invalid':form.errors.age}" id="age">
                                <span v-if="form.errors.age" class="invalid-feedback">{{ form.errors.age }}</span>
                            </div>
                            <div class="mb-3">
                                <label for="email" class="form-label">Avatar</label>
                                <input class="form-control" type="file" @input="form.avatar = $event.target.files[0]" :class="{'is-invalid':form.errors.avatar}"/>
                                <span v-if="form.errors.avatar" class="invalid-feedback">{{ form.errors.avatar }}</span>
                            </div>
                            <button type="submit" class="btn btn-primary">Save</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>

<script>

    import AppLayout from "../../Layouts/App.vue";
    import {
        Link
    } from '@inertiajs/inertia-vue'

    export default {
        components: {
            AppLayout,
            Link
        },
         props: {
            student: {
                type: Object,
                required: true
            }
        },
        data() {
            return {
                form: this.$inertia.form({
                    name: this.student.name,
                    email: this.student.email,
                    avatar: null,
                    _method: 'PUT'
                }),

                id: this.student.id,
            }
        },
        methods:{
            updateData(){
                console.log(this.form);
                this.form.post(route('students.update',this.id),{
                    onSuccess: (page) => {alert('Student Updated')},
                })
            }
        }
    }
</script>
