# banner


(function(){
var Banner={
    init:function(ele){
    this.banner=ele.a;
    this.bars=ele.b;
    this.length=$(this.banner+' li').length;
    this.dots=$(this.bars+' .dots');
    this.index=0;
    this.timer=null;
    if(this.length-1>0){
    for(var i=0;i<this.length;i++){
    this.dots.append('<span></span>');
    }
    }
    this.run();
    this.auto();
    $(this.bars+' .dots span,'+this.banner+' li').mouseover(function(){
    clearInterval(Banner.timer);
    }).mouseout(function(){
    Banner.auto();
    });
    $(this.bars+' .dots span').click(function(){
        Banner.index=$(this).index();
        Banner.run();
    });
    },
    auto:function(){
        var _this=this;
        this.timer=setInterval(function(){
        _this.per=(_this.index)*(-20)+'%';
        _this.index++;
        if(_this.index==_this.length){
        _this.index=1;
        };
        _this.run();
    },1000)
    },
    run:function(){
     //banner变化的两种展现形式
     $(this.banner).css("transform","translate3d("+this.per+",0,0)");
     //$(this.banner+' li').eq(this.index).css("display","block").siblings().css("display","none");
     $(this.bars+' .dots span').eq(this.index).addClass("active").siblings().removeClass();
    }
}
    Banner.init({
        'a':'.banner',
        'b':'.banner-box'
    });
})();
