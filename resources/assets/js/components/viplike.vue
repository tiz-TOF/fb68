<template>
    <div class="row">
        <div class="col-lg-6">
            <div class="panel panel-default">
                <div class="panel-heading">
                    <b><i class="fa fa-gears"></i> Panel Cài Đặt VIP Like</b>
                </div>
                <div class="panel-body">
                    <form action="" method="POST">
                        <div class="form-group">
                            <label>ID mới cần thêm:</label>
                            <input id="uid" placeholder="100004520190007" type="number" class="form-control" name="id" required="" autofocus="">
                        </div>
                        <div class="form-group">
                            <label>Số Lượng Like:</label>

                            <select name="package" id="package" class="form-control">
                                <option value="15">150 like(Reactions)</option>
                                <option value="30">300 like(Reactions)</option>
                                <option value="60">600 like(Reactions)</option>
                                <option value="100">1.000 like(Reactions)</option>
                                <option value="150">1.500 like(Reactions)</option>
                                <option value="200">2.000 like(Reactions)</option>
                                <option value="250">2.500 like(Reactions)</option>
                                <option value="300">3.000 like(Reactions)</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>Loại cảm xúc:</label>
                            <div class="text-center">
                                <label style="padding: 0 5px;" title="Gói VIP Like"><input checked="" type="checkbox" name="type[]" style="float: left;" value="LIKE" /> <span id="like"></span></label>
                                <label style="padding: 0 5px;" title="Gói VIP Cảm Xúc LOVE"><input type="checkbox" name="type[]" style="float: left;" value="LOVE" /><span id="love"></span></label>
                                <label style="padding: 0 5px;" title="Gói VIP Cảm Xúc WOW"><input type="checkbox" name="type[]" style="float: left;" value="WOW" /><span id="wow"></span></label>
                                <label style="padding: 0 5px;" title="Gói VIP Cảm Xúc HAHA"><input type="checkbox" name="type[]" style="float: left;" value="HAHA" /><span id="haha"></span></label>
                                <label style="padding: 0 5px;" title="Gói VIP Cảm Xúc SAD"><input type="checkbox" name="type[]" style="float: left;" value="SAD" /><span id="sad"></span></label>
                                <label style="padding: 0 5px;" title="Gói VIP Cảm Xúc ANGRY"><input type="checkbox" name="type[]" style="float: left;" value="ANGRY" /><span id="angry"></span></label>
                            </div>
                        </div>
                        <div class="form-group">
                            <label>Tốc Độ Like/5 Phút:</label>
                            <select name="solike" id="speed" class="form-control">
                                <option value="30">30 Like</option>
                                <option value="40">40 Like</option>
                                <option value="50">50 Like</option>
                                <option value="100">100 Like</option>

                            </select>
                        </div>
                        <div class="form-group">
                            <label>Thời Hạn:</label>
                            <select name="time" id="time" class="form-control">
                                <!--<option value="free">Free Test 1 Day</option>-->
                                <option value="15">15 Ngày (0.5 Tháng)</option>
                                <option value="30">30 Ngày (1 Tháng)</option>
                                <option value="45">45 Ngày (1.5 Tháng)</option>
                                <option value="60">60 Ngày (2 Tháng)</option>
                            </select>
                        </div>
                        Thành Tiền:
                        <div class="input-group">
                            <span class="input-group-addon">$</span>
                            <input type="text" disabled="disable" value="15000" class="form-control" id="thanhtien" />
                            <span class="input-group-addon">VNĐ</span>
                        </div>
                        <br>
                        <button type="button" class="btn btn-danger" v-on:click="install_viplike">Cài VIP Like</button>
                    </form>
                </div>
            </div>
        </div>
        <div class="col-lg-6">
            <div class="panel panel-default">
                <div class="panel-heading">
                    <b><i class="fa fa-gears"></i> Danh Sách ID VIP</b>
                </div>
                <div class="panel-body">
                    <div class="box-body table-responsive no-padding">
                        <table class="table table-hover">
                            <tbody>
                            <tr>
                                <th>ID VIP</th>
                                <th>Gói</th>
                                <th>Type</th>
                                <th>Hạn Sử Dụng</th>
                                <th>Active</th>
                            </tr>
                            <tr v-for="list in listVipID">
                                <td>{{list.uid}}</td>
                                <td>{{list.package}}</td>
                                <td>{{list.type}}</td>
                                <td>{{list.time}} Ngày</td>
                                <td><input type="checkbox" :checked="list.active == 1 ? 'checked':''" /> </td>
                            </tr>
                            </tbody></table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    data() {
        return {
            posts: [],
            errors: [],
            type:[],
            package: '',
            uid: '',
            speed: '',
            time: '',
            listVipID: [],
        }
    },
    methods:{
        install_viplike: function(){
            this.type = [];
            $('input[name="type[]"]:checked').each((i,e)=>{
                this.type.push($(e).val());
            });
            this.package = $('#package').val();
            this.uid = $('#uid').val();
            this.speed = $('#speed').val();
            this.time = $('#time').val();
            if(this.type == ''){
                toastr.error("Vui lòng chọn loại cảm xúc!");
                return false;
            }else if(this.package == ''){
                toastr.error("Vui lòng chọn gói cảm xúc!");
                return false;
            }else if(this.uid == ''){
                toastr.error("Vui lòng nhập UID!");
                return false;
            }else if(this.speed == ''){
                toastr.error("Vui lòng chọn loại thời gian cron!");
                return false;
            }else if(this.time == ''){
                toastr.error("Vui lòng chọn gói thời gian!");
                return false;
            }
            axios.post('api/installViplike',
                {
                    'uid':this.uid,
                    'type':this.type,
                    'package':this.package,
                    'speed':this.speed,
                    'time':this.time,
                }).then((response) => {
                if(response.data.success == 'true'){
                    toastr.success(response.data.message);
                }else{
                    toastr.error(response.data.message);
                }
            })
        }
    },
    mounted() {
        axios.get('api/getViplikeID').then((response) => {
            this.listVipID = response.data;
        })
    },
}
</script>