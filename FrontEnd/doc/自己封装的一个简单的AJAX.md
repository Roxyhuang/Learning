自己简单封装了一个AJAX
-- 

    //简单封装
     getAjaxData:function(ajaxConfig){
    var _this = this;
      return  $.ajax({
    type: ajaxConfig.type|| "GET",
    url:ajaxConfig.url ,
    data:ajaxConfig.data || {},
    dataType:ajaxConfig.dataType || "json"
    })
    },

    //调用实例
    var initajaxConfig ={
    type:"POST",
    url:"getMoreCampaign.htm",
    data:{
    numPerPage:15,
    pageNum:parseInt(document.querySelector("#currentPage").value)+1 || 1,
    orderFlag:_this.orderFlag
    }
    };
    //$(".main").loadMore(loadingConfig);
    _this.getAjaxData(initajaxConfig).done(function(data){
    if(data.flag==0){
    _this.campaignList = data.campaignList;
    _this.currentPage = "graph"
    }else{
    _this.currentPage = "noData"
    }
    });