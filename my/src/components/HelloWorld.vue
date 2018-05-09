<template>
  <div class="hello">
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      company:'',
      code:'',
      hostName:'',
    }
  },
  created(){
        this.hostName = location.hostname;
        let companyid=this.$route.query.company
        let code=this.$route.query.code
        this.company =  companyid
        this.code = code
        if(companyid!=null&&code!=null){
            this.getOpenid()
        }
        else{
            alert('处理出现错误');
            location.href='http://www.itchun.com';
        }
        
  },
  methods:{
    //获取用户openid
        getOpenid(){
            let that=this;
            this.$http.get('/api/product/order/weixin/user?companyId='+this.company+'&code='+this.code)
            .then(res=>{
                if(res.data.info.code){
                    let openid=res.data.info.openId;
                    location.href='http://www.itchun.com/login?openId='+openid+'&companyId='+this.company;
                }
                else{
                   alert(res.data.msg);
                }
            })
            .catch(err=>{
                alert('获取openid失败');
                console.log(err);
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
