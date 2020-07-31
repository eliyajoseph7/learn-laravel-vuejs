<template>
    <div class="container-fluid">
        <div class="card mt-3">
            <div class="card-header flex justify-content-between">
              <h3 class="card-title">DataTable with default features</h3>
              <button class="btn btn-primary float-right" @click="newModal">Add User <i class="fas fa-user-plus fa-fw"></i></button>
            </div>
            <!-- /.card-header -->
            <div class="card-body">
              <div id="example1_wrapper" class="dataTables_wrapper dt-bootstrap4">
                  <div class="row">
                  <div class="col-sm-12">
                  <table id="example1" class="table table-bordered table-striped dataTable dtr-inline collapsed table-responsive" role="grid" aria-describedby="example1_info">
                <thead>
                    <tr role="row">
                        <th class="sorting_asc" tabindex="0" aria-controls="example1" rowspan="1" colspan="1" aria-sort="ascending" aria-label="UserID: activate to sort column descending">UserID</th>
                        <th class="sorting" tabindex="0" aria-controls="example1" rowspan="1" colspan="1" aria-label="First Name: activate to sort column ascending">First Name</th>
                        <th class="sorting" tabindex="0" aria-controls="example1" rowspan="1" colspan="1" aria-label="Last Name: activate to sort column ascending">Last Name</th>
                        <th class="sorting" tabindex="0" aria-controls="example1" rowspan="1" colspan="1" aria-label="Phone(s): activate to sort column ascending">Phone</th>
                        <th class="sorting" tabindex="0" aria-controls="example1" rowspan="1" colspan="1" aria-label="Email version: activate to sort column ascending">Email</th>
                        <th class="sorting" tabindex="0" aria-controls="example1" rowspan="1" colspan="1" aria-label="Username: activate to sort column ascending">Username</th>
                        <th class="sorting" tabindex="0" aria-controls="example1" rowspan="1" colspan="1" aria-label="Gender: activate to sort column ascending">Gender</th>
                        <th class="sorting" tabindex="0" aria-controls="example1" rowspan="1" colspan="1" aria-label="Occupation: activate to sort column ascending">Occupation</th>
                        <th class="sorting" tabindex="0" aria-controls="example1" rowspan="1" colspan="1" aria-label="Permission: activate to sort column ascending">Permission</th>
                        <th class="sorting" tabindex="0" aria-controls="example1" rowspan="1" colspan="1" aria-label="Permission: activate to sort column ascending">Registered on</th>
                        <th class="sorting" tabindex="0" aria-controls="example1" rowspan="1" colspan="1" aria-label="Action: activate to sort column ascending">Action</th>
                    </tr>
                </thead>
                <tbody>
                                    
                    <tr role="row" class="odd" v-for="user in users" :key="user.id">
                        <td tabindex="0" class="sorting_1">{{ user.id }}</td>
                        <td>{{ user.firstname | upText }}</td>
                        <td>{{ user.lastname | upText }}</td>
                        <td>{{ user.email | upText}}</td>
                        <td>{{ user.phone }}</td>
                        <td>{{ user.username | upText}}</td>
                        <td>{{ user.gender }}</td>
                        <td>{{ user.occupation | upText }}</td>
                        <td>{{ user.permission | upText }}</td>
                        <td>{{ user.created_at | theDate }}</td>
                        <td>
                            <a href="#" @click="editModal(user)">
                                <i class="fa fa-user-edit fa-2x"></i>
                            </a>
                            <a href="#" @click="deleteUser(user.id)">
                                <i class="fas fa-trash-alt fa-2x text-danger"></i>
                            </a>
                        </td>
                    </tr>
                </tbody>
                <tfoot>
                    <tr>
                        <th rowspan="1" colspan="1">UserID</th>
                        <th rowspan="1" colspan="1">First Name</th>
                        <th rowspan="1" colspan="1">Last Name</th>
                        <th rowspan="1" colspan="1">Phone</th>
                        <th rowspan="1" colspan="1">Email</th>
                        <th rowspan="1" colspan="1">Username</th>
                        <th rowspan="1" colspan="1">Gender</th>
                        <th rowspan="1" colspan="1">Occupation</th>
                        <th rowspan="1" colspan="1">Permission</th>
                        <th rowspan="1" colspan="1">Registered on</th>
                        <th rowspan="1" colspan="1">Action</th>
                    </tr>
                </tfoot>
              </table></div></div><div class="row"><div class="col-sm-12 col-md-5"><div class="dataTables_info" id="example1_info" role="status" aria-live="polite">Showing 1 to 10 of 57 entries</div></div><div class="col-sm-12 col-md-7"><div class="dataTables_paginate paging_simple_numbers" id="example1_paginate"><ul class="pagination"><li class="paginate_button page-item previous disabled" id="example1_previous"><a href="#" aria-controls="example1" data-dt-idx="0" tabindex="0" class="page-link">Previous</a></li><li class="paginate_button page-item active"><a href="#" aria-controls="example1" data-dt-idx="1" tabindex="0" class="page-link">1</a></li><li class="paginate_button page-item "><a href="#" aria-controls="example1" data-dt-idx="2" tabindex="0" class="page-link">2</a></li><li class="paginate_button page-item "><a href="#" aria-controls="example1" data-dt-idx="3" tabindex="0" class="page-link">3</a></li><li class="paginate_button page-item "><a href="#" aria-controls="example1" data-dt-idx="4" tabindex="0" class="page-link">4</a></li><li class="paginate_button page-item "><a href="#" aria-controls="example1" data-dt-idx="5" tabindex="0" class="page-link">5</a></li><li class="paginate_button page-item "><a href="#" aria-controls="example1" data-dt-idx="6" tabindex="0" class="page-link">6</a></li><li class="paginate_button page-item next" id="example1_next"><a href="#" aria-controls="example1" data-dt-idx="7" tabindex="0" class="page-link">Next</a></li></ul></div></div></div></div>
            </div>
            <!-- /.card-body -->
          </div>


<!-- Modal -->
<div class="modal fade" id="addNew" tabindex="-1" role="dialog" aria-labelledby="addNewLabel" aria-hidden="true">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="addNewLabel">Add new user</h5>
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
      </div>
        <form @submit.prevent="createUser">
            <div class="modal-body">
                <div class="form-group">
                    <input v-model="form.firstname" type="text" name="firstname"
                        placeholder="First Name"
                        class="form-control" :class="{ 'is-invalid': form.errors.has('firstname') }">
                    <has-error :form="form" field="firstname"></has-error>
                </div>
                <div class="form-group">
                    <input v-model="form.lastname" type="text" name="lastname"
                        placeholder="Last Name"
                        class="form-control" :class="{ 'is-invalid': form.errors.has('lastname') }">
                    <has-error :form="form" field="lastname"></has-error>
                </div>
                <div class="form-group">
                    <input v-model="form.email" type="email" name="email"
                        placeholder="email"
                        class="form-control" :class="{ 'is-invalid': form.errors.has('email') }">
                    <has-error :form="form" field="email"></has-error>
                </div>
                <div class="form-group">
                    <input v-model="form.username" type="text" name="username"
                        placeholder="username"
                        class="form-control" :class="{ 'is-invalid': form.errors.has('username') }">
                    <has-error :form="form" field="username"></has-error>
                </div>
                <div class="form-group">
                    <input v-model="form.phone" type="tel" name="phone"
                        placeholder="+255123456789"
                        class="form-control" :class="{ 'is-invalid': form.errors.has('phone') }">
                    <has-error :form="form" field="phone"></has-error>
                </div>
                <div class="form-group">
                    <select v-model="form.gender" type="text" name="gender"
                        class="form-control" :class="{ 'is-invalid': form.errors.has('gender') }">
                        <option value=""> Select Gender </option>
                        <option value="M"> Male </option>
                        <option value="F"> Female </option>
                    </select>    
                    <has-error :form="form" field="gender"></has-error>
                </div>
                <div class="form-group">
                    <select v-model="form.occupation" type="text" name="occupation"
                        class="form-control" :class="{ 'is-invalid': form.errors.has('occupation') }">
                        <option value=""> Select occupation </option>
                        <option value="bill officer"> Bill Officer </option>
                        <option value="bill manager"> Bill Manager </option>
                        <option value="accountant"> Accountant </option>
                    </select>    
                    <has-error :form="form" field="occupation"></has-error>
                </div>
                <div class="form-group">
                    <select v-model="form.permission" type="text" name="permission"
                        class="form-control" :class="{ 'is-invalid': form.errors.has('permission') }">
                        <option value=""> Select permission </option>
                        <option value="superuser"> Superuser </option>
                        <option value="user"> Normal user </option>
                    </select>    
                    <has-error :form="form" field="permission"></has-error>
                </div>
                <div class="form-group">
                    <input v-model="form.password" type="password" name="password"
                        placeholder="password"
                        class="form-control" :class="{ 'is-invalid': form.errors.has('password') }">
                    <has-error :form="form" field="password"></has-error>
                </div>
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                <button type="submit" class="btn btn-primary">Create User</button>
            </div>
        </form>
    </div>
  </div>
</div>
    </div>
</template>

<script>
    export default {
        data() {
            return{
                users: {},
                form: new Form({
                    firstname: '',
                    lastname: '',
                    email: '',
                    phone: '',
                    username: '',
                    gender: '',
                    occupation: '',
                    permission: '',
                    password: '',
                })
            }
        },
        methods: {
            editModal(user){
                this.form.reset();
                $('#addNew').modal('show');
                this.form.fill(user);
            },
            newModal(){
                this.form.reset();
                $('#addNew').modal('show');
            },
            deleteUser(id){
                Swal.fire({
                    title: 'Are you sure?',
                    text: "You won't be able to revert this!",
                    icon: 'warning',
                    showCancelButton: true,
                    confirmButtonColor: '#3085d6',
                    cancelButtonColor: '#d33',
                    confirmButtonText: 'Yes, delete it!'
                    }).then((result) => {
                        if(result.value){
                            this.form.delete(`api/user/${id}`).then(()=> {
                                    Swal.fire(
                                        'Deleted!',
                                        'Your file has been deleted.',
                                        'success'
                                    )
                                    Fire.$emit('afterCreate')
                            }).catch(()=> {
                                Swal.fire({
                                    icon: 'error',
                                    title: 'Oops...',
                                    text: 'Something went wrong!',
                                    footer: '<a href>Why do I have this issue?</a>'
                                })
                            })
                        }
                })
            },
            loadUsers(){
                axios.get('api/user').then(({data}) => (this.users = data))
            },
            createUser() {
                this.$Progress.start()
                this.form.post('api/user')
                .then(()=> {
                    Fire.$emit('afterCreate')
    
                    $('#addNew').modal('hide');
    
                    Toast.fire({
                        icon: 'success',
                        title: 'User created successfully'
                    })
    
                    this.$Progress.finish()
                })
                .catch(()=> {

                })
            }
        },
        created() {
            this.loadUsers();
            Fire.$on('afterCreate', () => this.loadUsers())
        }
    }
</script>
