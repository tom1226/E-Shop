<template>

	<el-menu class="el-menu-vertical-demo" unique-opened router background-color="#545c64" text-color="#fff" active-text-color="#ffd04b" :collapse="isCollapse">
		<el-submenu index="1">
			<template slot="title">
				<i class="el-icon-notebook-1"></i>
				<span>商品管理</span>
			</template>
			<el-menu-item-group>
				<el-menu-item index="/goods/category">商品分类</el-menu-item>
				<el-menu-item index="/goods/release">发布商品</el-menu-item>
				<el-menu-item index="/goods/list">商品列表</el-menu-item>
			</el-menu-item-group>
		</el-submenu>

		<el-submenu index="2">
			<template slot="title">
				<i class="el-icon-setting"></i>
				<span>订单管理</span>
			</template>
			<el-menu-item-group>
				<el-menu-item index="/order/list">订单列表</el-menu-item>
			</el-menu-item-group>
		</el-submenu>

		<el-submenu index="3">
			<template slot="title">
				<i class="el-icon-user"></i>
				<span>账户设置</span>
			</template>
			<el-menu-item-group>
				<el-menu-item index="/account/infos">账户信息</el-menu-item>
			</el-menu-item-group>
		</el-submenu>

		<el-submenu index="4">
			<template slot="title">
				<i class="el-icon-set-up"></i>
				<span>用户管理</span>
			</template>
			<el-menu-item-group>
				<el-menu-item index="/user/list">用户列表</el-menu-item>
			</el-menu-item-group>
		</el-submenu>

		<el-submenu index="6">
			<template slot="title">
				<i class="el-icon-connection"></i>
				<span>权限设置</span>
			</template>
			<el-menu-item-group>
				<el-menu-item index="/power/role">用户角色</el-menu-item>
				<el-menu-item index="/power/menu">菜单权限</el-menu-item>
			</el-menu-item-group>
		</el-submenu>

	</el-menu>

</template>

<script>
	import { mapState } from 'vuex';
	export default{
		data(){
			return{
				
			}
		},
		computed:{			
			...mapState('menu',['isCollapse'])
		},
	}
</script>

<style lang="less" scoped="scoped">
	.el-menu-vertical-demo {
		height: 100%;
		overflow: hidden;
	}
	 .el-menu-vertical-demo:not(.el-menu--collapse) {
	    width: 200px;
	    height: 100%;
		overflow: hidden;
	  }
</style>
