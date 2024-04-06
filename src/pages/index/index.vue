<template>
	<view class="content">
        <image class="logo" src="../../static/logo.png"></image>
		<view>
            <text class="title">{{title}}</text>
        </view>
	</view>
</template>

<script lang="ts">
  import Vue from 'vue';
  import cv, { Mat, Rect } from "opencv-ts";

  // import cv from '@/uni_modules/zj-opencv';

	export default Vue.extend({
		data() {
			return {
				title: 'Hello66'
			}
		},
		onLoad() {
// cv.then(async () => {
//     const src = await cv.imread('first');
//     const dst = new cv.Mat();
//     cv.cvtColor(src, dst, cv.COLOR_RGBA2GRAY, 0);
//     await cv.imshow('second', dst);
    // src.delete();
    // dst.delete();
// });
cv.onRuntimeInitialized = () => {
    const src = cv.imread("inputCanvas");
    const dst: Mat = new cv.Mat(src.cols, src.rows, cv.CV_8UC4);

    cv.resize(src, dst, new cv.Size(500, 500), 0, 0, cv.INTER_AREA);

    const roiRect: Rect = new cv.Rect(0, 0, 200, 200);

    const roi = dst.roi(roiRect);

    cv.imshow('outputCanvas', roi);
};
		},
		methods: {

		}
	});
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin: 200rpx auto 50rpx auto;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
