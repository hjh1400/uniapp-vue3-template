<template>
  <view>
    <view class="flex items-center bg-white pb-30rpx pl-30rpx pr-20rpx">
      <u-form :model="form" ref="uForm">
        <u-form-item label="姓名"><u-input v-model="form.name" /></u-form-item>
        <u-form-item label="手机号"><u-input v-model="form.phoneCode" /></u-form-item>
        <view class="section">
          <view class="section__title">预约日期</view>
          <picker :bindchange="bindPickerChange" :value="index" :range="array">
            <view class="picker">
              预约日期：{{array[index]}}
            </view>
          </picker>
        </view>
        <u-form-item label="预约时间">
          <u-radio-group :model="value" @change="radioGroupChange">
            <u-radio
              @change="radioChange"
              v-for="(item, index) in list" :key="index"
              :name="item.name"
              :disabled="item.disabled"
              :label="item.name"
            ></u-radio>
          </u-radio-group>
        </u-form-item>
      </u-form>
    </view>


  </view>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: '',
        intro: '',
        sex: ''
      },
      title: 'picker',
      array: ['中国', '美国', '巴西', '日本'],
      index: 0,
      date: new Date(),
      time: '12:01',
      checkboxList: [
        {
          name: '苹果',
          checked: false,
          disabled: false
        },
        {
          name: '雪梨',
          checked: false,
          disabled: false
        },
        {
          name: '柠檬',
          checked: false,
          disabled: false
        }
      ],
      radioList: [
        {
          name: '鲜甜',
          disabled: false
        },
        {
          name: '麻辣',
          disabled: false
        }
      ],
      radio: '',
      switchVal: false,
      list: [
        {
          name: 'apple',
          disabled: false
        },
        {
          name: 'banner',
          disabled: false
        },
        {
          name: 'orange',
          disabled: false
        }
      ],
      // u-radio-group的v-model绑定的值如果设置为某个radio的name，就会被默认选中
      value: 'orange',
      show: true,
      lists: [
        [
          {
            value: '1',
            label: '江'
          },
          {
            value: '2',
            label: '湖'
          }
        ],
        [
          {
            value: '3',
            label: '夜'
          },
          {
            value: '4',
            label: '雨'
          }
        ],

      ],
    };
  },methods:{
    // 回调参数为包含多个元素的数组，每个元素分别反应每一列的选择情况
    confirm(e) {
      console.log(e);
    }, bindPickerChange: function(e) {
      console.log('picker发送选择改变，携带值为', e.detail.value)
      this.index = e.detail.value
    },
    bindDateChange: function(e) {
      this.date = e.detail.value
    },
    bindTimeChange: function(e) {
      this.time = e.detail.value
    },
    getDate(type) {
      const date = new Date();
      let year = date.getFullYear();
      let month = date.getMonth() + 1;
      let day = date.getDate();

      if (type === 'start') {
        year = year - 60;
      } else if (type === 'end') {
        year = year + 2;
      }
      month = month > 9 ? month : '0' + month;
      day = day > 9 ? day : '0' + day;
      return `${year}-${month}-${day}`;
    }
  }
};
</script>

<style lang="scss" scoped>
.login-form-wrap {
  margin: 80rpx auto 0;
  width: 400rpx;

  .title {
    margin-bottom: 100rpx;
    font-size: 60rpx;
    text-align: left;
    font-weight: 500;
  }

  input {
    padding-bottom: 6rpx;
    margin-bottom: 10rpx;
    text-align: left;
  }

  .tips {
    margin-top: 8rpx;
    margin-bottom: 60rpx;
    color: $u-info;
  }

  .login-btn {
    padding: 12rpx 0;
    font-size: 30rpx;
    color: $u-tips-color;
    background-color: rgb(253 243 208);
    border: none;

    &::after {
      border: none;
    }
  }

  .alternative {
    display: flex;
    justify-content: space-between;
    margin-top: 30rpx;
    color: $u-tips-color;
  }
}

.login-type-wrap {
  display: flex;
  justify-content: space-between;
  padding: 350rpx 150rpx 150rpx;

  .item {
    display: flex;
    align-items: center;
    font-size: 28rpx;
    color: $u-content-color;
    flex-direction: column;
  }
}

.hint {
  padding: 20rpx 40rpx;
  font-size: 20rpx;
  color: $u-tips-color;

  .link {
    color: $u-warning;
  }
}

.picker{
  padding: 13px;
  background-color: #FFFFFF;
}
.page {
  padding-top: 80px;
}
</style>
