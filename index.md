<!DOCTYPE html>
<html>
<head>
	<title></title>
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<style type="text/css">
		.unlimit{
		    transition: none;
		    -webkit-animation: rotating 0.6s linear infinite;
		    -moz-animation: rotating 0.6s linear infinite;
		    -ms-animation: rotating 0.6s linear infinite;
		    -o-animation: rotating 0.6s linear infinite;
		    animation: rotating 0.6s linear infinite;
		  }

		@-webkit-keyframes rotating
		/*Safari and Chrome */
		{
		  to {
		    -ms-transform: rotate(0deg);
		    -moz-transform: rotate(0deg);
		    -webkit-transform: rotate(0deg);
		    -o-transform: rotate(0deg);
		    transform: rotate(0deg);
		  }
		  from {
		    -ms-transform: rotate(360deg);
		    -moz-transform: rotate(360deg);
		    -webkit-transform: rotate(360deg);
		    -o-transform: rotate(360deg);
		    transform: rotate(360deg);
		  }
		}
		@keyframes rotating {
		  to {
		    -ms-transform: rotate(0deg);
		    -moz-transform: rotate(0deg);
		    -webkit-transform: rotate(0deg);
		    -o-transform: rotate(0deg);
		    transform: rotate(0deg);
		  }
		  from {
		    -ms-transform: rotate(360deg);
		    -moz-transform: rotate(360deg);
		    -webkit-transform: rotate(360deg);
		    -o-transform: rotate(360deg);
		    transform: rotate(360deg);
		  }
		}
	</style>
	<style type="text/css">
		.col-xs-12 {
		    width: 100%;
		}
		.vongxoay-img {
		    background: url('vong-quay-all.png') no-repeat;
		    background-position: -5px 41px;
		    height: 520px;
		}
		.vongxoay-img img:nth-child(1) {
		    position: relative;
		    margin-top: 80px;
		}
		.vongxoay-img img:nth-child(2) {
		    position: absolute;
		    margin: 40px -173px;
		}
		body{
			margin: 0;
			padding:0;
		}
	</style>
	<script type="text/javascript" src="jquery.min.js"></script>
</head>
<body>
	<div class="col-xs-12 col-sm-5 col-md-5 col-lg-5 vongxoay-img" id="vongxoaytichdiem">
        <img src="vong-quay-circle.png" alt="" id="img_quay">
        <img src="vong-quay-target.png">
    </div>
    <p id="ketqua"></p>
    <a style="font-size: 25px;color: #000;" href="javascript: void(0)" onclick="quay();" class="vtaui-btn-blue">Quay ngay</a>
   	<script type="text/javascript">
   		var hieu_ung = {
			'el': '#img_quay',
			'stop_point': null,
			'interval_id': null,
			'stop_index': {
				1:[0], //50 Vpoint
				2:[30], //20 Vpoint
				3:[60,180,300],  //5 Vpoint
				4:[90,210], //90 - Mặt mếu , 210 - Mặt cười
				5:[120],   //40 Vpoint
				6:[150], //10 Vpoint
				7:[240], //30 Vpoint
				8:[270], //10 Vpoint
		        9:[330]  // flower
			},
			'rotate_count': 5,
			'old_point' : {
				'check' : false,
				'value_old' : null,
				'value_new' : null
			},

			'play': function()
			{
				if (!this.stop_point)
					return;
				// if(this.old_point.check){
				// 	console.log(this.stop_point)
				// 	this.stop_point;
				// }
				if(this.old_point.value_old == null){
					this.old_point.value_old = this.old_point.value_new;
				}
				
				$(this).css('-webkit-transform', 'rotate('+this.old_point.value_old+'deg)');
				$(this).css('-moz-transform', 'rotate('+this.old_point.value_old+'deg)');
				$(this).css('transform', 'rotate('+this.old_point.value_old+'deg)');
				//console.log('Giá trị v_old : ' + this.old_point.value_old);

				var v_old = this.old_point.value_old;
				var v_stop = this.stop_point;
				var element = this.el;
				var v_this = this;

				//setTimeout(function(){
					//console.log(this.old_point.value_old);
					//v_stop = v_stop + (360 - v_old);
					//console.log(this.stop_point);
					//console.log(v_stop)
					$(this.el).animate({  transform: v_stop }, {
					    step: function(now,fx) {
							fx.start = v_old;
							//console.log(now);
							// if(now == 0){
							// 	now = v_old;
							// }
							//cubic-bezier(1,0,0,1)
							if(now >= v_old){
								$(this).css('-webkit-transform','rotate('+now+'deg)'); 
								$(this).css('-moz-transform','rotate('+now+'deg)');
								$(this).css('transform','rotate('+now+'deg)');
							}
					    },
					    duration: 5000
					}, 'ease-out'
					);
				//},0)
				
			},
			'stop': function ()
			{
				$(this.el).stop();
			},
			'setStopPoint': function(params)
			{
				if(this.stop_point != null){
					this.old_point.check = true;
				}
				var arr_point = this.stop_index[params.coupon_id];
				
				
				//console.log(this.stop_point)
				var valueArrPoint = arr_point[Math.floor(Math.random() * arr_point.length)];
				console.log('Giá trị tọa độ : ' + valueArrPoint);
				this.stop_point = this.rotate_count*360 + valueArrPoint;
				//console.log(this.stop_point);
				if(this.old_point.check){
					//if(this.old_point.value_old == null)
					this.old_point.value_old = this.old_point.value_new;
					this.old_point.value_new = valueArrPoint;
					//console.log(this.old_point.value);
				}else{
					this.old_point.value_old = 0;
					this.old_point.value_new = valueArrPoint;
				}
			}
		};
   	</script>
   	<script type="text/javascript">

        var isBusying = false;
        function quay() {
            if (!isBusying) {
                //$('#img_quay').addClass('unlimit');
                isBusying = true;
                var response = {
					"Successfully": true,
					"Status": null,
					"GiftPart": {
						"Id": 0,
						"Point": 30,
						"Name": Math.floor(Math.random() * 9) + 1,//"5",
						"Label": "30",
						"Frequency": 0,
						"CampaignId": null
				  	},
				  	"TotalPoint": 0
				}
                setTimeout(function(){
                	if(1 == 1){
                		if (response.Successfully) {
                            hieu_ung.setStopPoint({ 'coupon_id': response.GiftPart.Name });
                            //$('#img_quay').removeClass('unlimit');
                            $('#ketqua').html('.');
                            hieu_ung.play();
                            //setTimeout(function () { alert("Chúc mừng bạn đã được tích " + response.Data.Name + " điểm vào tài khoản."); isBusying = false; }, 9000);
                            setTimeout(function () {
                                isBusying = false;
                                var messageResult = 'Bạn nhận được ';
                                /*
                                1:[0], //50 Vpoint
								2:[30], //20 Vpoint
								3:[60,180,300],  //5 Vpoint
								4:[90,210], //90 - Mặt mếu , 210 - Mặt cười
								5:[120],   //40 Vpoint
								6:[150], //10 Vpoint
								7:[240], //30 Vpoint
								8:[270], //10 Vpoint
						        9:[330]  // flower
						        */
                                switch(response.GiftPart.Name){
                                	case 1:
                                		messageResult = messageResult + '50 Vpoint';
                                		break;
                                	case 2:
                                		messageResult = messageResult + '20 Vpoint';
                                		break;
                                	case 3:
                                		messageResult = messageResult + '5 Vpoint';
                                		break;
                                	case 4:
                                		messageResult = messageResult + 'Hên xui';
                                		break;
                                	case 5:
                                		messageResult = messageResult + '40 Vpoint';
                                		break;
                                	case 6:
                                		messageResult = messageResult + '10 Vpoint';
                                		break;
                                	case 7:
                                		messageResult = messageResult + '30 Vpoint';
                                		break;
                                	case 8:
                                		messageResult = messageResult + '10 Vpoint';
                                		break;
                                	case 9:
                                		messageResult = messageResult + 'flower';
                                		break;
                                	default :
                                		messageResult = 'Error!';
                                		break;
                                }
                                $('#ketqua').html(messageResult);
                            }, 5000);
                        } else {
                            var messageResult = "Không thành công!";
                            // if (response.Status === "Campaign_DoAction_BeLimitedMaximumPlayInDay") {
                            //     messageResult = "<p>Hôm nay bạn đã tham gia vòng quay may mắn</p> <p class='strong-title'>Vui lòng quay lại sau</p>";
                            // }
                            $('#ketqua').html(messageResult);
                            isBusying = false;
                        }
                	}else{
                		isBusying = false;
                	}
                },0)
                
                // $.ajax({
                //     url: '/loyaltygetpoint/quay?_ultoken=26e44fa6-da7a-4e9a-9760-c11a5fc94250',
                //     type: 'GET',
                //     success: function (response) {
                //         //console.log(response);
                //         if (response.Successfully) {
                //             hieu_ung.setStopPoint({ 'coupon_id': response.GiftPart.Name });
                //             //$('#img_quay').removeClass('unlimit');
                //             hieu_ung.play();
                //             //setTimeout(function () { alert("Chúc mừng bạn đã được tích " + response.Data.Name + " điểm vào tài khoản."); isBusying = false; }, 9000);
                //             setTimeout(function () {
                //                 showGiftPart(response.GiftPart.Label, response.TotalPoint);
                //                 isBusying = false;
                //                 $("#clickpopup").trigger("click");
                //             }, 9000);
                //         } else {
                //             var message = "Không thành công!";
                //             if (response.Status === "Campaign_DoAction_BeLimitedMaximumPlayInDay") {
                //                 message = "<p>Hôm nay bạn đã tham gia vòng quay may mắn</p> <p class='strong-title'>Vui lòng quay lại sau</p>";
                //             }
                //             //console.log(response.Status);
                //             VtaGlobal.VtaFancyboxHtmlContent(message, 'vta-popup-notification vtaui-bg-icon-smile');
                //             isBusying = false;
                //         }
                //     },
                //     fail: function () {
                //         isBusying = false;
                //     },
                //     complete: function () {
                //     }
                // });
            }
        }
    </script>
</body>
</html>
