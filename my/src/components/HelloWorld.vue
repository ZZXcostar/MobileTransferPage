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
      recommendedTeamId:'',
      recommendedAdminId:'',
      presentationStr:''
    }
  },
  created(){
     //  alert(window.location.href)
        let datas=JSON.parse(this.$route.query.json);

        this.hostName = location.hostname;
        // let companyid=this.$route.query.company
        // let code=this.$route.query.code;
        // let recommendedTeamId=this.$route.query.recommendedTeamId;
        // let recommendedAdminId=this.$route.query.recommendedAdminId;
        let companyid=datas.company
        let code=this.$route.query.code;
        let recommendedTeamId=datas.recommendedTeamId;
        let recommendedAdminId=datas.recommendedAdminId;
        let presentation = datas.presentation;

        this.company =  companyid
        this.code = code
        this.recommendedTeamId=recommendedTeamId;
        this.recommendedAdminId=recommendedAdminId;
        this.presentationStr = presentation
        
        if(companyid!=null&&code!=null){
            this.getOpenid()
        }
        else{
            alert('处理出现错误');
            location.href='http://www.shhongzhiyun.com';
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

                   // alert(that.presentationStr)
                    if(that.presentationStr == "isPresentation"){
                      location.href='http://www.shhongzhiyun.com/presentationLogin?openId='+openid+'&company='+that.company+'&recommendedTeamId='+that.recommendedTeamId+'&recommendedAdminId='+that.recommendedAdminId;
                    }else{
                      location.href='http://www.shhongzhiyun.com/login?openId='+openid+'&company='+that.company+'&recommendedTeamId='+that.recommendedTeamId+'&recommendedAdminId='+that.recommendedAdminId;
                    }   
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
