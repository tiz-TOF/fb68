<template>
    <div class="row">
        <div class="col-lg-6">
            <div class="panel panel-default">
                <div class="panel-heading">
                    <b><i class="fa fa-gears"></i> Thông Tin Cá Nhân</b>
                </div>
                <div class="panel-body">
                    <div class="form-group">
                        <label>Email</label>
                        <input type="text" class="form-control" :value="this.$parent.info.email" disabled=""/>
                    </div>
                    <div class="form-group">
                        <label>Fbid</label>
                        <input type="text" class="form-control" :value="this.$parent.info.fbid" disabled=""/>
                    </div>
                    <div class="form-group">
                        <label>Tài Khoản</label>
                        <input type="text" class="form-control" :value="this.$parent.info.money" disabled=""/>
                    </div>
                    <div class="form-group">
                        <label>Name</label>
                        <input type="text" class="form-control" :value="this.$parent.info.name" />
                    </div>
                </div>
            </div>
        </div>
        <div class="col-lg-6">
            <div class="panel panel-default">
                <div class="panel-heading">
                    <b><i class="fa fa-gears"></i> Lịch Sử Giao Dịch</b>
                </div>
                <div class="panel-body">
                    <div id="example1_wrapper" class="dataTables_wrapper form-inline dt-bootstrap no-footer">
                        <div class="row">
                            <div class="col-sm-12">
                                <table class="table table-bordered">
                                    <tr role="row">
                                        <th>ID </th>
                                        <th>Loại Giao Dịch</th>
                                        <th>Số Tiền</th>
                                        <th>Note</th>
                                        <th>Thời Gian</th>
                                    </tr>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>

</script>