<template>
  <div class="hello">
    <button>点击测试</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      company:'',
      code:''
    }
  },
  created(){
      let companyid=this.$route.query.company
      let code=this.$route.query.code
      this.company =  companyid
      this.code = code
       if(companyid!=null){
            sessionStorage.setItem('companyId',companyid);
        }
        if(code!=null){
            this.getOpenid().then(flag=>{
                if(flag){
                    if(this.$route.params.logining!=null&&this.$route.params.logining){
                        this.selected='我的';
                        this.$router.push('/login');
                    }
                }
            });
        }
        else{
            if(sessionStorage.getItem('openId')==null){
                alert('请授权后再登录商城');
            }
        }
        
  },
  methods:{
    //获取用户openid
        getOpenid(){
           return  new Promise((resolve,reject)=>{
                let that=this;
                this.$http.get('/api/product/order/weixin/user?companyId='+this.company+'&code='+this.code)
                .then(res=>{
                    if(res.data.info.code){
                        let openid=res.data.info.openId;
                        sessionStorage.setItem('openId',openid);
                        resolve(true);
                    }
                    else{
                        resolve(false);
                         alert(res.data.msg);
                        // Toast('xxx');
                    }
                })
                .catch(err=>{
                    alert('获取openid失败');
                    console.log(err);
                    resolve(false);
                })
            })
            
        }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
