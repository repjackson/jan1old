<template>
  <admin-content>
    <admin-sidebar></admin-sidebar>
    <div class="admin-content_main">
      <header class="admin-content_main-header">
      	<h2 class="title">Users</h2>
      </header>	
      <el-table
		    :data="users"
		    border
		    style="width: 100%"
		    class="admin-content_main-table">
		    <el-table-column
		      label="Created At"
		      width="220">
		      <template slot-scope="scope">
		        <el-icon class="icon" name="time"></el-icon>
		        <span>{{ scope.row.createdAt | date("L, LT") }}</span>
		      </template>
		    </el-table-column>
		    <el-table-column
		      label="Name">
		      <template slot-scope="scope">
						<span>{{ scope.row.profile.firstName }} {{ scope.row.profile.lastName }}</span>
		      </template>
		    </el-table-column>
		    <el-table-column
		      label="Phone"
		      width="220">
		      <template slot-scope="scope">
		        <svg class="icon">
	            <use xlink:href="/icons.svg#mobile" />
	          </svg>
		        <span>{{ scope.row.profile.phone }}</span>
		      </template>
		    </el-table-column>
		    <el-table-column
		      label="Actions">
		      <template slot-scope="scope">
		        <el-button
		          size="small"
		          @click="handleEdit(scope.$index, scope.row)">Edit</el-button>
		        <el-button
		          size="small"
		          type="danger"
		          @click="handleDelete(scope.$index, scope.row)">Delete</el-button>
		      </template>
		    </el-table-column>
		  </el-table>
    </div>
  </admin-content>
</template>

<script>
  export default {
  	name: 'admin-users',
  	data: () => ({
      users: []
    }),
  	meteor: {
      subscribe: {
        'users': [],
      },
      users() {
        return Meteor.users.find({})
      },
    },
    methods: {
    	 handleEdit (index, row) {
        this.$router.push({
          name: 'admin-users-edit',
          params: { userId: row._id }
        })
      },
      async handleDelete (index, row) {
        try {
          await Meteor.callPromise('Users.methods.remove', {
            _id: row._id
          })
          this.$message({
            type: 'info',
            message: 'User removed!'
          })
        } catch (error) {
          this.$message({
            type: 'error',
            message: error
          })
        }
      },
    },
    components: {
    }
  }
</script>
