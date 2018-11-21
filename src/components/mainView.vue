<template>
  <div>
    <div class="styleEditor" ref="sty">
      <pre>
        {{strInput}}
      </pre>
      <div v-html="htmlInput">

      </div>
    </div>
    <div class="resumeEditor">
      <div v-html="resumeInput">

      </div>
    </div>
  </div>
</template>

<script>
    export default {
      name: "mainView",
      data(){
        return{

          count:0,
          resumeCount:0,
          //vw==view-width vh==view-height(视窗宽高)
          strWait:[`
          /*我是冯帆,这是我的个人简历
           *简历写起来太单调了,我想让它动起来
           *Just do it
           */

           /*首先先加个背景吧*/
           html {
             color: rgb(222,222,222); background: rgb(0,43,54);
           }
           /* 有点生硬,我们加点过渡效果 */
            * {
              transition: all 0.5s;
            }
            /* 文字离边框太近了 */
            .styleEditor {
              padding: 0.5em;
              border: 1px solid;
              margin: 1em;
              overflow: auto;
              width: 45vw; height: 90vh;
            }
            /* 加点 3D 效果呗 */
             html{
               perspective: 1000px;
             }
             .styleEditor {
                position: fixed; left: 0; top: 0;
                -webkit-transition: none;
                transition: none;
                -webkit-transform: rotateY(10deg) translateZ(-100px) ;
                transform: rotateY(10deg) translateZ(-100px) ;
             }
             /* 下面我准备了一个IDE */
              .resumeEditor{
                position: fixed; right: 0; top: 0;
                padding: 0.5em 2em 0.5em 2em;  margin: 1em;
                width: 45vw; height: 90vh;
                border: 1px solid;
                background: white; color: #222;
                overflow: auto;
              }
              /* 好了，我要开始写简历了 */
          `,`
            <h3>姓名 : 冯帆</h3>
            <h3>年龄 : 24</h3>
            <h3>学习经历 : 合肥工业大学</h3>
            <h3>所在地 : 北京</h3>
            <h3>技能 :</h3>
            <ul>
            <li>前端开发 : Html Css Javascript Jquery Vue.js Bootstrap</li>
            <li>后端开发 : Node.js</li>
            <li>开发工具 : Gulp Webpack Sass</li>
            <li>调试工具 : fiddler</li>
            </ul>
            <h3>联系方式:</h3>
            <ul>
                <li>电子邮箱 :<a href="mailto:243327096@qq.com"> 243327096@qq.com</a></li>
                <li>联系电话 :<a href="tel:18632215896"> 18632215896</a></li>
                <li>Github :<a href="https://github.com/fengfan0409" target="_blank"> 点击进入</a></li>
            </ul>
          `]

        }
      },
      methods:{
        inp:function () {
          //Vue里this指向发生改变时,用箭头函数解决!
          let timeIn=setInterval(()=> {
            if (this.strWait[0]===this.strInput){
              clearInterval(timeIn);
              this.resumeInp()
            }
            this.count++;
            this.$refs.sty.scrollTop=10000;//自动下滑
        },30)
        },
        resumeInp:function () {
          let timeOut=setInterval(()=>{
            if (this.strWait[1]===this.resumeInput){
              clearInterval(timeOut)
            }
            this.resumeCount++;
          },1)
        }
      },
      mounted(){
        this.inp()
      },
      //computed下要是obj,不可以function
      computed:{
        htmlInput(){
          return '<style>'+this.strWait[0].slice(0,this.count)+'</style>'
        },
        strInput(){
          return this.strWait[0].slice(0,this.count)
        },
        resumeInput(){
          return this.strWait[1].slice(0,this.resumeCount)
        }
      }
    }
</script>

<style scoped>

</style>
