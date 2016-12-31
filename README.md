# HTML
<div id="wrapper">
    <div class="container">
        <div class="row">
            <div class="col-lg-12">
                <h1>Coin Flip | <span>Global or Fortune</span></h1>
            </div>
            <div class="col-lg-12">
                <!--blank-->
                <div class="col-lg-4"></div>
                <!--coin-->
                <div class="col-lg-4">
                    <div class="coinBox">
                        <div class="tail">
                            <img src="coin_F.png" />
                        </div>
                        <div class="head">
                            <img src="coin_G.png" />
                        </div>
                    </div>
                </div>
                <!--user form elements-->
                <div class="col-lg-4 text-left">
                        <p>
                        <div class="userChoice">
                          <button name="Global">Global</button>
                          <button name="Fortune">Fortune</button>
                        </div>
                        <p>
                            <button class="btn btn-lg btn-primary" id="btnFlip" disabled>Flip It</button>
                        </p>
                </div>
            </div>
        </div>
    </div>
</div>

#CSS

#wrapper 
{
    width: 100%;
    height: auto;
    min-height: 500px;
}

.btn
{
    width: 12%;
    background-color: #c34f4f;
    color: white;
    padding: 14px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 22px;
}

.btn:hover
{
    background-color: #A64242;
}

input[type=submit]:hover {
    background-color: #A64242;
}

.container
{
    padding: 50px 0;
    text-align: center;
}

h1
{
    margin-bottom: 100px;
}

.head
{
    margin-top: -205px;
}

.flip img{animation: flipIt 0.5s linear infinite;}
.head img
{
    animation-delay: 0.25s;
}

@keyframes flipIt
{
    0%{width: 0px;
        height: 200px;}
    25%{width: 200px;
        height: 200px;}
    50%{width: 0px;
        height: 200px;}
    100%{width: 0px;
        height: 200px;}
}
.disableclick {
  pointer-events: none;
}

#JQUERY

var result,userchoice;
function resetAll(){
    var resetHTML = '<div class="tail"><img src="coin_F.png" /></div><div class="head"><img src="coin_G.png" /></div>';
    setTimeout(function(){
        $('.coinBox').fadeOut('slow',function(){
            $(this).html(resetHTML)
        }).fadeIn('slow',function(){
            $('#btnFlip').removeAttr('disabled');
        });
    },2500);
}
// Checking User Input
$(document).on('click','button[name="Global"],button[name="Fortune"]', function(){
    userchoice = $(this).attr("name");
    if(userchoice == "") {
        $(this).parent('p').prepend("<span class='text text-danger'>Please select a coin side to play the game</span>")
        $('#btnFlip').attr('disabled','disabled');
    } else {
        /**/
        $('#btnFlip').removeAttr('disabled');
        $(this).siblings('span').empty();
    }
    return userchoice;
});
// Final result declaration
function finalResult(result,userchoice){
    var resFormat = '<h3>';
    resFormat += '<span class="text text-primary">You choose : <u>'+userchoice+'</u></span> |';
    resFormat += '<span class="text text-danger"> Result : <u>'+result+'</u></span>';
    resFormat += '</h3>';
    var winr = '<h2 class="text text-success" style="color: #49DF3E;">You Won!!</h2>';
    var losr = '<h2 class="text text-danger" style="color: #c34f4f;">You Lost...</h2>';
    if(result == userchoice){
        $('.coinBox').append(resFormat+winr)
    } else{
        $('.coinBox').append(resFormat+losr)
    }
}
// Button Click Actions
$(document).on('click','#btnFlip',function() {
    if($('#userChoice').val() == "") return;
    var flipr = $('.coinBox>div').addClass('flip');
    var number = Math.floor(Math.random()*2);
    $(this).attr('disabled','disabled').addClass('disableclick');
    var button = $(this);
    setTimeout(function() {
        flipr.removeClass('flip');
        button.removeClass('disableclick');
        //result time
        if(number) {
            result = 'Global';
        //alert('Head = '+number);
            $('.coinBox').html('<img src="coin_G.png" /><h3 class="text-primary">Global</h3>');
            finalResult(result,userchoice);
            resetAll();
        } else {
            result = 'Fortune';
        //alert('Tail = '+number);
            $('.coinBox').html('<img src="coin_F.png" /><h3 class="text-primary">Fortune</h3>');
            finalResult(result,userchoice);
            resetAll();
        }
    },2000);
    return false;
});
