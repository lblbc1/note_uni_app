//厦门大学计算机专业 | 前华为工程师
//专注《零基础学编程系列》  http://lblbc.cn/blog
//包含：Java | 安卓 | 前端 | Flutter | iOS | 小程序 | 鸿蒙
//公众号：蓝不蓝编程
<template>
    <view class="page-wrapper">
        <form @submit="onSubmit">
            <scroll-view :scroll-y="true">
				<view class="info-container">
				    <view class="common-info-row">
				        <textarea class="common-input" name="content" placeholder="请输入正文" :value="content"></textarea>
				    </view>
				</view>
				
            </scroll-view>
            <view class="bottom-wrapper">
                <button class="bottom-btn" form-type="submit">确定</button>
            </view>
        </form>
    </view>
</template>

<script>
import { queryNote, modifyNote } from '@/common/api'
export default {
    data() {
        return {
			id: 0,
            content: '',
        };
    },
    onLoad: function (option) {
        this.queryData(option.id);
    },
    methods: {
        queryData(noteId) {
			this.id = noteId
			queryNote(noteId).then(resp => {
				if (!resp.data.code) {
					this.content = resp.data.data.content
				}
			})
        },

        onSubmit(e) {
            var params = {
                content: e.detail.value.content,
            };
			modifyNote(this.id, params).then(resp => {
				if (!resp.data.code) {
					uni.navigateBack();
				}
			})
        },
    }
};
</script>
<style>
page {
    background-color: #f4f4f4;
}

.page-wrapper {
    margin: 0;
    font-size: 32rpx;
    line-height: 1.5;
    color: #333;
    overflow-x: hidden;
    -webkit-overflow-scrolling: touch;
    -webkit-tap-highlight-color: transparent;
    min-height: 2000rpx;
}
.split {
    background-color: #e0e3ea;
    height: 2rpx;
    margin: 20rpx 10rpx;
}
.info-container {
    background-color: #fff;
    border-radius: 10rpx;
    margin-top: 40rpx;
    margin-left: 20rpx;
    margin-right: 20rpx;
    padding-left: 20rpx;
    padding-right: 20rpx;
    padding-top: 20rpx;
    padding-bottom: 20rpx;
}
.common-info-row {
    display: flex;
    flex-direction: row;
    margin-top: 20rpx;
    margin-bottom: 20rpx;
    align-items: center;
}
.common-info {
}
.common-input {
    margin-left: 20rpx;
}
.bottom-wrapper {
    position: fixed;
    bottom: 0;
    width: 100%;
}
.bottom-btn {
    font-size: 30rpx;
    color: #fff;
    margin: 50rpx 50rpx;
    background-color: #418DF9;
    border-radius: 2rem;
}
</style>
