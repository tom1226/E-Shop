<template>
	<el-upload class="avatar-uploader" :headers="header" action="http://localhost:3003/api/upload/common" :data="{type:type}" :show-file-list="false"
	 :on-success="handleAvatarSuccess" :before-upload="beforeAvatarUpload">
		<template v-if="url">
			<img :src="url" class="avatar">
			<i @click.stop="handleRemove" class="el-icon-delete avatar-uploader-remove"></i>
		</template>
		<i v-else class="el-icon-plus avatar-uploader-icon"></i>
	</el-upload>
</template>
<!-- http://localhost:3003/api/upload/goods -->
<script>
	import { Upload } from '@/api/index';

	export default {
		props: ['url','type'],
		data() {
			return{
				header: {
					Authorization: `Bearer ${sessionStorage.token}`
				}
			}
		},
		methods: {
			async handleRemove() {
				// 判断是否默认头像
				let isDefault = this.url.indexOf('default') >= 0;

				if (isDefault) {
					this.$emit('update:url','');
					return false;
				}
				let { status } = await Upload.remove({ src: this.url });
				if (status) {
					this.$message.success("删除成功！");
					this.$emit('update:url','')
				}
			},
			handleAvatarSuccess(res, file, fileList) {
				if (res.status) {
					this.$message.success(res.msg);
					this.$emit('success', res);
					this.$emit('update:url',res.src)
				}else{
					console.log(res);
					console.log(file);
					console.log(fileList);
				}
			},
			 handleAvatarError(err,file,filelist){
				if(err){
					let res = JSOn.parent(err.message);
					this.$message.success(msg)
				}
			},
			beforeAvatarUpload(file) {
				const isJPG = file.type === 'image/jpeg';
				const isLt2M = file.size / 1024 / 1024 < 2;
				if (!isJPG) {
					this.$message.error('上传头像图片只能是 JPG 格式!');
				}
				if (!isLt2M) {
					this.$message.error('上传头像图片大小不能超过 2MB!');
				}
				return isJPG && isLt2M;
			},
		}
	}
</script>

<style lang="less">
	.avatar-uploader{
		display: inline-block;
	}
	.avatar-uploader .el-upload {
		border: 1px dashed #d9d9d9;
		border-radius: 6px;
		cursor: pointer;
		position: relative;
		overflow: hidden;
		box-sizing: border-box;
		line-height: normal!important;
	}
	.el-card .el-form .avatar-uploader{
		.avatar {
			width: 178px;
			height: 178px;
			display: block;
		}
	}
	.avatar-uploader .el-upload:hover {
		border-color: #409EFF;
	}

	.avatar-uploader-icon,
	.avatar-uploader-remove {
		font-size: 28px;
		color: #8c939d;
		width: 178px;
		height: 178px;
		line-height: 178px;
		text-align: center;
	}

	

	.avatar-uploader:hover .avatar-uploader-remove {
		display: block;
	}

	.avatar-uploader-remove {
		position: absolute;
		left: 0;
		top: 0;
		color: white;
		background-color: rgba(0, 0, 0, 0.7);
		display: none;
		z-index: 10;
	}
</style>
