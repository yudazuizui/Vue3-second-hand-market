<template>
  <div class="main">
    <div class="home">校园二手跳蚤市场</div>
    <div class="body">
      <div class="big">
        <div class="box">登记中心</div>
        <input type="text" placeholder="请输入商品名称" v-model="shangpin" />
        <div class="leixing">请选择类型</div>
        <select class="opi" v-model="leixing">
          <!-- <option disabled value="">请选择类型</option> -->
          <option>电子产品</option>
          <option>书籍</option>
          <option>学习用品</option>
          <option>其它</option>
        </select>
        <div class="price">预期价格</div>
        <input
          type="text"
          class="money"
          placeholder="心里预期价格"
          v-model="jiage"
        />
        <textarea
          name=""
          id=""
          cols="30"
          rows="5"
          class="area"
          placeholder="请输入卖品描述"
          v-model="miaoshu"
        ></textarea>
        <div class="">联系方式</div>
        <input
          type="text"
          class="connect"
          placeholder="请输入联系方式"
          v-model="lianxi"
        />
        <button class="pic">
          <input @change="uploadFile($event)" type="file" ref="input" />
        </button>
        <button class="login" @click="login">登记</button>
        <button class="reset" @click="reset">重置</button>
      </div>
    </div>
    <!-- 展示数据-->
    <div class="footer">
      <div v-for="(item, index) in paimai" key="index" @click="showindex">
        <div class="show">
          <div class="remake">名称：{{ item.shangpin }}</div>
          <div class="solid">商品类型：{{ item.leixing }}</div>
          <div class="solidprice">卖家价格：{{ item.jiage }}</div>
          <div class="connect">卖家联系方式：{{ item.lianxi }}</div>
          <div class="describe">商品描述：</div>
          <textarea cols="30" rows="5" class="desarea" disabled>{{
            item.miaoshu
          }}</textarea>
          <div class="view" v-show="item.tupian">卖品图片展示：</div>
          <img
            :src="item.tupian"
            style="width: 9.375rem; height: 6.25rem"
            v-show="item.tupian"
          />
          <button class="delete" @click="delete1(index)">删除</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup >
import { ref } from 'vue'
// 商品名称
const shangpin = ref('')
// 商品类型
const leixing = ref('')
// 预期价格
const jiage = ref('')
// 商品描述
const miaoshu = ref('')
// 联系方式
const lianxi = ref('')
// 上传的图片
const tupian = ref('')
// 定义一个空数组用于后面展示登记的商品列表
const paimai = ref([])
// 获取input标签
const input = ref('')
// 删除按钮的作用
const delete1 = (i) => {
  paimai.value.splice(i, 1)
}
// 登记按钮的作用
const login = () => {
  paimai.value.push({ shangpin: shangpin.value, leixing: leixing.value, jiage: jiage.value, miaoshu: miaoshu.value, lianxi: lianxi.value, tupian: tupian.value })
  reset()
}
// 重置按钮的作用
const reset = () => {
  shangpin.value = '',
    leixing.value = '',
    jiage.value = '',
    miaoshu.value = '',
    lianxi.value = '',
    tupian.value = ''
  input.value.value = ''
  // console.log(input.value)

}
const uploadFile = (el) => {
  if (!el.target.files[0].size) return // 如果文件大小为0，则返回
  if (el.target.files[0].type.indexOf('image') === -1) { //如果不是图片格式
    console.log('请选择图片文件')
  } else {
    const reader = new FileReader() // 创建读取文件对象
    reader.readAsDataURL(el.target.files[0]) // 发起异步请求，读取文件
    reader.onload = function () {  // 文件读取完成后
      // 读取完成后，将结果赋值给img的src
      tupian.value = this.result
    }
  }
}

</script>

<style lang="less" scoped>
.footer {
  // display: flex;
  width: 100vw;
  // flex-wrap: wrap;
  // justify-content: space-evenly;
  // padding: 50px;
  .show {
    width: 100vw;
    height: 29.375rem;
    background-color: paleturquoise;
    padding: 0.625px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    // margin-right: 25px;
    margin-top: 1.875rem;
    .solid {
      padding: 0.625rem;
    }
    .solidprice {
      padding: 0.625rem;
    }
    .connect {
      padding: 0.625rem;
    }
    .delete {
      width: 2.1875rem;
      height: 1.875rem;
      background-color: red;
      border-radius: 0.1875rem;
      border: none;
      cursor: pointer;
    }
    .describe {
      padding: 0.3125rem;
    }
    .desarea {
      margin: 0.625rem;
      width: 12.5rem;
      height: 5rem;
      background-color: #fff;
    }
    img {
      margin: 0.625rem 0;
    }
  }
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  border: 0;
}
html,
body {
  background-color: #eee;
}
.home {
  margin: auto;
  width: 12.5rem;
  margin-top: 1.875rem;
  height: 5rem;
  text-align: center;
  font-size: 1.5625rem;
  color: red;
}
.body {
  position: relative;
  margin-top: 1.25rem;
  width: 100vw;
  height: 26.875rem;
  background-color: antiquewhite;
  .money {
    width: 6.25rem;
    margin-bottom: 0.375rem;
    vertical-align: center;
  }
  input::-webkit-input-placeholder {
    padding-left: 0.3125rem;
  }
  .pic {
    display: block;
    margin: 0 auto;
    text-align: center;
    margin: 0.4375rem auto;
    background-color: pink;
    color: #eee;
    border: none;
    width: 4.375rem;
    cursor: pointer;
    border-radius: 0.1875rem;
  }

  .area {
    padding: 0.125rem;
  }
  textarea:focus {
    outline: none;
  }
  input:focus {
    outline: none;
  }
  .box {
    padding: 0.625rem 0;
    color: red;
  }
  .login {
    padding: 0.625rem 0.375rem;
    font-size: 1.125rem;
    margin-right: 1.25rem;
    cursor: pointer;
    border-radius: 0.3125rem;
    border: none;
  }
  .reset {
    padding: 10px 6px;
    font-size: 18px;
    cursor: pointer;
    border: none;
    border-radius: 5px;
  }
  .big {
    position: absolute;
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
    width: 18.75rem;
    height: 23.75rem;
    text-align: center;
    padding: 0.625rem;
    background-color: pink;
  }
  .opi {
    margin: 0.1875rem 0;
  }
}
</style>