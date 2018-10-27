<template>
    <div class="login-form">
        <div class="form-item">
            <label class="item-label">用户名：</label>
            <div class="itme-input">
                <input type="text" v-model="usernameModel" placeholder="请输入用户名">
            </div>
            <span class="item-error">{{ userErrors.errorText }}</span>
        </div>
        <div class="form-item">
            <label class="itme-label">密码：</label>
            <div class="itme-input">
                <input type="password" v-model="passwordModel" placeholder="请输入密码">
            </div>
            <span class="item-error">{{ passwordErrors.errorText }}</span>
        </div>
        <input type="button" value="登录" @click="onLogin" />
        <div>{{ globalErrorText }}</div>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                usernameModel: '',
                passwordModel: '',
                globalErrorText: ''
            }
        },
        methods: {
            onLogin () {
                if (!this.userErrors.status || !this.passwordErrors/status) {
                    this.globalErrorText = '请输入填写完整'
                } else {
                    this.globalErrorText = ''
                    this.$http.get('api/login')
                    .then((res) => {
                        this.$emit('has-log', res.data.data)
                    }, (error) => {
                        console.log(error)
                    })
                }
            }
        },
        computed: {
            userErrors () {
                let errorText, status
                if (!/@/g.test(this.usernameModel)) {
                    status = false,
                    errorText = '不包含@'
                } else {
                    status = true,
                    errorText = ''
                }
                if (!this.userFlag) {
                    errorText = ''
                    this.userFlag = true
                }
                return  {
                    status,
                    errorText
                }
            },
            passwordErrors () {
                let errorText, status
                if (!/^\w{1,6}$/g.test(this.passwordModel)) {
                    status = false,
                    errorText = '密码不是1-6位'
                } else {
                    status = true,
                    errorText = ''
                }
                if (!this.passwrodFlag) {
                    errorText = ''
                    this.passwrodFlag = true
                }
                return  {
                    status,
                    errorText
                }
            }
        }
    }
</script>
