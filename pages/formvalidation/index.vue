<template>
    <div>
        <div class="container">
            <form @submit.prevent="onSubmit">
                <div class="form-group">
                    <!-- First Name -->
                    <label for="exampleInputFirstName">First Name</label>
                    <!-- <input v-model="v$.form.firstName.$model" type="text" class="form-control" :class="{'is-invalid': v$.form.firstName.$errors.length}" id="exampleInputFirstName" placeholder="Enter First Name"> -->
                    <input v-model="v$.form.firstName.$model" type="text" class="form-control" :class="v$.form.firstName.$errors.length ? 'is-invalid' : (form.firstName ? 'is-valid' : '')" id="exampleInputFirstName" placeholder="Enter First Name">
                    
                    <!-- error message -->
                    <div class="invalid-feedback" v-for="(error, index) of v$.form.firstName.$errors" :key="index">
                        <span>{{ error.$message }}</span>
                    </div>
                </div>
                <div class="form-group">
                    <!-- Last Name -->
                    <label for="exampleInputLastName">Last Name</label>
                    <!-- <input v-model="v$.form.lastName.$model" type="text" class="form-control" :class="{'is-invalid': v$.form.lastName.$errors.length}" id="exampleInputLastName" placeholder="Enter Last Name"> -->
                    <input v-model="v$.form.lastName.$model" type="text" class="form-control" :class=" v$.form.lastName.$errors.length ? 'is-invalid' : (form.lastName ? 'is-valid' : '')" id="exampleInputLastName" placeholder="Enter Last Name">
                    
                    <!-- error message -->
                    <div class="invalid-feedback" v-for="(error, index) of v$.form.lastName.$errors" :key="index">
                        <span>{{ error.$message }}</span>
                    </div>
                </div>
                <div class="form-group">
                    <!-- Email -->
                    <label for="exampleInputEmail1">Email address</label>
                    <!-- <input v-model="v$.form.email.$model" type="email" class="form-control" :class="{'is-invalid': v$.form.email.$errors.length}" aria-describedby="emailHelp" placeholder="Enter email"> -->
                    <input v-model="v$.form.email.$model" type="email" class="form-control" :class=" v$.form.email.$errors.length ? 'is-invalid' : (form.email ? 'is-valid' : '')" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter email">
                    <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
                    
                    <!-- error message -->
                    <div class="invalid-feedback" v-for="(error, index) of v$.form.email.$errors" :key="index">
                        <span>{{ error.$message }}</span>
                    </div>
                </div>
                <div class="form-group">
                    <!-- Password -->
                    <label for="exampleInputPassword1">Password</label>
                    <!-- <input v-model="v$.form.password.$model" type="password" class="form-control" :class="{'is-invalid': v$.form.password.$errors.length}" id="exampleInputPassword1" placeholder="Password"> -->
                    <input v-model="v$.form.password.$model" type="password" class="form-control" :class=" v$.form.password.$errors.length ? 'is-invalid' : (form.password ? 'is-valid' : '')" id="exampleInputPassword1" placeholder="Password">
                    
                    <!-- error message -->
                    <div class="invalid-feedback" v-for="(error, index) of v$.form.password.$errors" :key="index">
                        <div class="error-msg">{{ error.$message }}</div>
                    </div>
                </div>
                <div class="form-group">
                    <!-- Confirm Password -->
                    <label for="exampleInputPassword2">Confirm Password</label>
                    <!-- <input v-model="v$.form.confirmPassword.$model" type="password" class="form-control" :class="{'is-invalid': v$.form.confirmPassword.$errors.length}" id="exampleInputPassword2" placeholder="Confirm Password"> -->
                    <input v-model="v$.form.confirmPassword.$model" type="password" class="form-control" :class=" v$.form.confirmPassword.$errors.length ? 'is-invalid' : (form.confirmPassword ? 'is-valid' : '')" id="exampleInputPassword2" placeholder="Confirm Password">
                    
                    <!-- error message -->
                    <div class="invalid-feedback" v-for="(error, index) of v$.form.confirmPassword.$errors" :key="index">
                        <span>{{ error.$message }}</span>
                    </div>
                </div>
                <div class="form-check">
                    <!-- <input v-model="v$.form.acceptTerms.$model" type="checkbox" class="form-check-input" :class="{'is-invalid': v$.form.acceptTerms.$errors.length}" id="exampleCheck1"> -->
                    <input v-model="v$.form.acceptTerms.$model" type="checkbox" class="form-check-input" :class=" v$.form.acceptTerms.$errors.length ? 'is-invalid' : (form.acceptTerms ? 'is-valid' : '')" id="exampleCheck1">
                    <label class="form-check-label" for="exampleCheck1">Check me out</label>
                    
                    <!-- error message -->
                    <div class="invalid-feedback" v-for="(error, index) of v$.form.email.$errors" :key="index">
                        <span>{{ error.$message }}</span>
                    </div>
                </div>
                <button type="submit" class="btn btn-primary">Submit</button>
            </form>
        </div>
    </div>
</template>

<script>
    import useVuelidate from '@vuelidate/core'
    import { required, email, minLength, sameAs } from '@vuelidate/validators'
    export default {
        setup () {
            return { v$: useVuelidate() }
        },
        head() {
            return {
                title: "Form Validation", 
            };
        },
        data() {
            return {
                form: {
                    firstName: "",
                    lastName: "",
                    email: "",
                    password: "",
                    confirmPassword: "",
                    acceptTerms: false,
                },
            }
        },
        validations() {
            return {
                form: {
                    firstName: {required},
                    lastName: {required},
                    email: {required, email},
                    password: {
                        required,
                        min: minLength(6)
                    },
                    confirmPassword: {
                        required,
                        min: minLength(6),
                        matched: sameAs(this.form.password)
                    },
                    acceptTerms: {
                        checked: sameAs(true)
                    },
                }
            }
        },
        methods: {
            onSubmit(e) {
                this.v$.$validate().then( (response) => {
                    if (response) {
                        console.log('Submited Successfully');
                    } else {
                        console.log('Submit Failed !');
                    }
                });
            },
        }
    }
</script>

