表单优化
========
建议把填写的input放进table里，用表单形式展现出来
-------------------------------------------------

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">










<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>online form</title>
<!--
<link rel="stylesheet" type="text/css" href="/web/css/style.css">
<link rel="stylesheet" type="text/css" href="/web/css/form.css">
-->
<link href="../css/style.css" rel="stylesheet" type="text/css" />
<link href="../css/validationEngine.jquery.css" rel="stylesheet" type="text/css" />


<script type="text/javascript" src="/web/js/mootools.js"></script>
<script type="text/javascript" src="/web/js/calendar.js"></script>
<script type="text/javascript" src="/web/js/utils.js"></script>
<script type="text/javascript" src="/web/js/jquery-1.8.3.js"></script>
	<script type="text/javascript" src="/web/js/jquery.validationEngine.js"></script>
	<script type="text/javascript" src="/web/js/jquery.validationEngine-en.js"></script>
<script type="text/javascript" src="/web/js/jquery.maskedinput-1.3.js"></script>
<script type="text/javascript">
	//<![CDATA[
	window.addEvent('domready', function() {
		myCal2 = new Calendar({ date: 'd/m/Y' }, { classes: ['dashboard'], direction: 1, tweak: {x: 3, y: -3} });
	});
	//]]>
var _$= jQuery.noConflict();
_$().ready(function($) {
  $("#form1").validationEngine({
	promptPosition: "centerRight",
	'custom_error_messages': {
					// Custom Error Messages for Validation Types
					'required': {
						'message': "不能为空!"
					}
					,'maxSize': {
						'message': "输入数据超过长度限制"
					}
					,'custom[date]': {
						'message': "日期格式不正确!"
					}
					,'ajax[ajaxCheckVerifyingCode]': {
						'message': "验证码不正确!"
					}
					,'#surname': {
						'custom[onlyLetterNumberS]': {
							'message': "姓名只能填写英文或数字!"
						}
					}
					,'#middleName': {
						'custom[onlyLetterNumberS]': {
							'message': "姓名只能填写英文或数字!"
						}
					}
					,'#givenName': {
						'custom[onlyLetterNumberS]': {
							'message': "姓名只能填写英文或数字!"
						}
					}
					,'condRequired': {
						'message': "不能为空!"
					}
					,'#passportNumber': {
						'custom[onlyLetterNumber]': {
							'message': "护照号码只能填入英文或者数字!"
						}
					}
				}
  });
  initMsg();
 });

jQuery(function($){
   $("input#dateOfBirth").mask("9999-99-99",{completed:function(){document.getElementById("dateOfBirth").value=this.val();}});
   //alert("You typed the following: "+document.getElementById("dateOfBirth").value);
});

function checkDate(){
	//alert("You typed the following: "+document.getElementById("dateOfBirth").value);
	var strDate = document.getElementById("dateOfBirth").value;
    var regex = new RegExp("^(?:(?:([0-9]{4}(-|\/)(?:(?:0?[1,3-9]|1[0-2])(-|\/)(?:29|30)|((?:0?[13578]|1[02])(-|\/)31)))|([0-9]{4}(-|\/)(?:0?[1-9]|1[0-2])(-|\/)(?:0?[1-9]|1\\d|2[0-8]))|(((?:(\\d\\d(?:0[48]|[2468][048]|[13579][26]))|(?:0[48]00|[2468][048]00|[13579][26]00))(-|\/)0?2(-|\/)29))))$");
	if (!regex.test(strDate)){
		//alert("日期格式不正确!");
		document.getElementById("dateOfBirth").value="";
		//document.form1.dateOfBirth.focus();
	}
}

function initMsg(){

	var msg = '';
	if(msg=="1"){
		alert('保存成功！申请表编号 ' + document.getElementById("appNo").value + '，请记录申请表编号，以便下次通过此编号调取表格继续填写并提交。请注意未提交的申请表本网站仅保存30天，请在上述时限内完成填表，提交并打印。');
	}
	document.getElementById("nameInChineseCheck").title='不适用';
	document.getElementById("formerNameCheck").title='不适用';
	//document.getElementById("nameInEthnicScriptCheck").title='不适用';
	document.getElementById("formerNationalityCheck").title='不适用';
	//document.getElementById("dualNationalityCheck").title='不适用';
	document.getElementById("idNumberCheck").title='不适用';
	if(document.getElementById("formerNameCheck").checked){
		getEl("formerName").value = "N/A";
		getEl("formerName").readOnly="true";
	}
	if(document.getElementById("nameInChineseCheck").checked){
		getEl("nameInChinese").value = "N/A";
		getEl("nameInChinese").readOnly="true";
	}
	//if(document.getElementById("nameInEthnicScriptCheck").checked){
	//	getEl("nameInEthnicScript").value = "N/A";
	//	getEl("nameInEthnicScript").readOnly="true";
	//}
	if(document.getElementById("formerNationalityCheck").checked){
		getEl("formerNationality").value = "N/A";
		getEl("formerNationality").readOnly="true";
	}
	//if(document.getElementById("dualNationalityCheck").checked){
	//	getEl("dualNationality").value = "N/A";
	//	getEl("dualNationality").readOnly="true";
	//}
	if(document.getElementById("idNumberCheck").checked){
		getEl("idNumber").value = "N/A";
		getEl("idNumber").readOnly="true";
	}
	//showTextDiv();
}
function checkChange(){
	if(document.getElementById("formerNameCheck").checked){
		getEl("formerName").value = "N/A";
		getEl("formerName").readOnly="true";
	}else{
		if(getEl("formerName").value == "N/A"){
			getEl("formerName").value = "";
		}
		getEl("formerName").readOnly = "";
	}
	if(document.getElementById("nameInChineseCheck").checked){
		getEl("nameInChinese").value = "N/A";
		getEl("nameInChinese").readOnly="true";
	}else{
		if(getEl("nameInChinese").value == "N/A"){
			getEl("nameInChinese").value = "";
		}
		getEl("nameInChinese").readOnly = "";
	}
	//if(document.getElementById("nameInEthnicScriptCheck").checked){
	//	getEl("nameInEthnicScript").value = "N/A";
	//	getEl("nameInEthnicScript").readOnly = "true";
	//}else{
	//	if(getEl("nameInEthnicScript").value == "N/A"){
	//		getEl("nameInEthnicScript").value = "";
	//	}
	//	getEl("nameInEthnicScript").readOnly = "";
	//}
	if(document.getElementById("formerNationalityCheck").checked){
		getEl("formerNationality").value = "N/A";
		getEl("formerNationality").readOnly = "true";
	}else{
		if(getEl("formerNationality").value == "N/A"){
			getEl("formerNationality").value = "";
		}
		getEl("formerNationality").readOnly = "";
	}
	//if(document.getElementById("dualNationalityCheck").checked){
	//	getEl("dualNationality").value = "N/A";
	//	getEl("dualNationality").readOnly = "true";
	//}else{
	//	if(getEl("dualNationality").value == "N/A"){
	//		getEl("dualNationality").value = "";
	//	}
	//	getEl("dualNationality").readOnly = "";
	//}
	if(document.getElementById("idNumberCheck").checked){
		getEl("idNumber").value = "N/A";
		getEl("idNumber").readOnly = "true";
	}else{
		if(getEl("idNumber").value == "N/A"){
			getEl("idNumber").value = "";
		}
		getEl("idNumber").readOnly = "";
	}
}
function nextForm(form1){
	//alert(getEl("dateOfBirth").value);
	form1.action="/web/applicationdata/ApplicationApply_formP2.action";
	jQuery('#form1').submit();
	//form1.submit();
}
function saveTemp(form1){
	form1.action="/web/applicationdata/ApplicationApply_saveTemp.action";
	form1.submit();
	//if(!window.confirm('保存成功！申请表编号' + document.getElementById("appNo").value + '，请记录申请表编号，以便下次通过此编号调取表格继续填写并提交。请注意未提交的申请表本网站仅保存30天，请在上述时限内完成填表，提交并打印。')){
	//	return;
	//	}
}

function expfile(form1){
	form1.action="/web/applicationdata/ApplicationApply_expfile.action";
	form1.submit();
}
function cl(){
	if(window.confirm("你确定继续这个操作?")){
		self.close();
	}
}
function showDiv(obj){
	if(obj.options[obj.selectedIndex].value=="CHN"){
		getEl("chinaDiv").style.display="block";
	}else{
		getEl("chinaDiv").style.display="none";
	}
}
function showTextDiv(){
	if(getEl("countryOfBirth").value.toUpperCase()=="CHN"){
		getEl("chinaDiv").style.display="block";
	}else{
		getEl("chinaDiv").style.display="none";
	}
}
function loadCity(){
	var url="/web/ajax/AppFormActionAjax_loadCity.action";
  	var parameters="language=zh_CN&provinceCode="+document.getElementById("provinceOfBirth").value;
  	callAjax2({url:url,paras:parameters,async:false,cbMethod:loadCityCb, type:"json"});
}
function loadCityCb(responseObj){
	//var resp = responseObj.responseText;
  	//var respObj = eval("("+resp+")");
  	var respObj = responseObj; //modify by mz

	if(respObj.actionErrorMsgList!=null||respObj.fieldsErrorMsgMap!=null)
    {
	    handleAjaxRespError(document.form,respObj.actionErrorMsgList,respObj.fieldsErrorMsgMap);
		return;
    }
  	var list = respObj.cityList;
  	var myobj=document.getElementById("cityOfBirth");
  	optionClearListObj(myobj);
  	for(n=0;n<list.length;n++)
  	{
  		//add("cityList",list[n][0],list[n][1]);
  		optionAddChildNode(myobj,list[n][0],list[n][1]);
  	}
}
function refreshHelp(field,evt){
	//var url="/web/helptext/HelpText_gethelp.action";
  	//var parameters="helpField="+field;
    //var url="https://www.visaforchina.org/PAR_ZH/online_help/"+field +".html";
    var light=document.getElementById("helpdiv");
    var _event = window.event || evt;
    if(_event.pageX || _event.pageY){
    	//alert("light.style.left=" + _event.pageX + "light.style.top" + _event.pageY);
    	//alert(document.documentElement.scrollTop + "++++++" + light.offsetHeight);
    	//light.style.left=_event.pageX + "px";
		light.style.top=_event.pageY - light.offsetHeight*1.5 + "px";
    }else{
    	//alert(_event.clientY + "++++++" + light.offsetHeight);
   		//light.style.left=_event.clientX + document.documentElement.clientLeft - document.documentElement.scrollLeft;
		light.style.top=_event.clientY + document.documentElement.scrollTop - light.offsetHeight*1.5 + "px";
    }
    //light.style.display='block';
    var url="https://www.visaforchina.org/PAR_ZH/online_help/"+field +".html";
    var parameters="";
  	callAjax2({url:url,paras:parameters,async:false,cbMethod:refreshHelpDiv, type:"text"});

}

function refreshHelpDiv(responseObj){
	var resp = responseObj;
	document.getElementById("helptext").innerHTML=resp;
}

</script>

</head>

<body>
<div class="worp">
<div class=" chamidbox">
	<!-- <div class="stepGu_logo"></div> -->
	<div class="stepGu_logo"><a href="https://www.visaforchina.org/YTO_ZH/" ><img src="/web/images/logo-qdf.png" /></a></div>
	</div><!-- header end-->
	<div class=" chamidboxbotttom"></div>
	<div class="footer2top"></div>



<div id="contentbg">


<div id="formstep">

  <div id="steplink7">
    <ul>
      <li  class="stepdone7"><table  border="0" cellspacing="0" cellpadding="0"><tr><td><span>开始</span></td></tr></table></li>

      <li class="stephere7 ml2"><table  border="0" cellspacing="0" cellpadding="0"><tr><td><span>个人信息</span></td></tr></table></li>







      <li class="ml2 stepnext7"><table  border="0" cellspacing="0" cellpadding="0"><tr><td><span>赴华旅行信息</span></td></tr></table></li>

      	 <!--



      <li class="ml2 stepnext7"><table  border="0" cellspacing="0" cellpadding="0"><tr><td><span>家庭、工作或学习信息</span></td></tr></table></li>

       -->



      <li class="ml2 stepnext7"><table  border="0" cellspacing="0" cellpadding="0"><tr><td><span>其他情况</span></td></tr></table></li>





      <li class="ml2 stepnext7"><table  border="0" cellspacing="0" cellpadding="0"><tr><td><span>声明和补充信息</span></td></tr></table></li>



    </ul><div class="stepbarbtn"></div>
  </div>



</div>

  <div id="formcontent">
  <div class="contentbox780">
  	<form id="form1" name="form1" action="/web/applicationdata/ApplicationApply_formP2.action" method="post">
  	<input type="hidden" name="operation" value="formP1" id="form1_operation"/>

  	<input type="hidden" id="appNo" name="appNo" value="0003604990"/>

    <div id="applicationid" class="mt10">
    申请表编号<span style="color:#ff9900; margin-left:20px;">0003604990</span>
    </div>
<!--
    <div id="formmain" >
      <div id="formalt">一、申请人个人信息</div>
      <div id="formline">
        若护照上有偕行人，且该偕行人要与您一起申请中国签证，请选择“是”<br />
        <div class="formcheck4">
          <p><input type="radio" data-validation-engine="validate[required] radio" data-prompt-position="centerRight:+180" name="someoneAcc" id="someoneAccYes"  value="1"/><label for="someoneAccYes">是</label>&nbsp&nbsp</p>
		  <p><input type="radio" data-validation-engine="validate[required] radio" data-prompt-position="centerRight:+180" name="someoneAcc" id="someoneAccNo"  value="0"/><label for="someoneAccNo">否</label>
         </p></div>
       	<br/>
        若申请表由他人代填，请选择“是” <br />
        <div  class="formcheck4">
         <p><input type="radio" data-validation-engine="validate[required] radio" data-prompt-position="centerRight:+180" name="othersDelegation" id="othersDelegationYes"  value="1"/><label for="othersDelegationYes">是</label>&nbsp&nbsp
		 </p>
		 <p><input type="radio" data-validation-engine="validate[required] radio" data-prompt-position="centerRight:+180" name="othersDelegation" id="othersDelegationNo"  value="0"/><label for="othersDelegationNo">否</label>
         </p>
         </div>
        <br/>
      </div>
       -->

      <!--

     -->
     <div id="formalt">一、申请人个人信息
      </div>

     <div class="formpad1 mt10">
     <div class="formleftpad">
     <div class="formsubtitle">1.1 护照中的英文姓名</div>
     <div class="formsubbox">
     申请人姓<br />
        <input type="text" name="surname" maxlength="39" value="" id="surname" class="inputtext" style="width:380px" data-validation-engine="validate[maxSize[39],custom[onlyLetterNumberS]]"/>

         <br />
        中间名<br />
        <input type="text" name="middleName" maxlength="39" value="" id="middleName" class="inputtext" style="width:380px" data-validation-engine="validate[maxSize[39],custom[onlyLetterNumberS]]"/>
        <br />
        名<br />
        <input type="text" name="givenName" maxlength="39" value="" id="givenName" class="inputtext" style="width:380px" data-validation-engine="validate[required,maxSize[39],custom[onlyLetterNumberS]]"/>
       <!-- <br /> -->

     </div>

     </div>

     <div class="helppad">
     <div class="helptext">
     请填写你护照上的英文姓名，并将姓与名分开。
	</div>
     </div>
     </div>

     <div class="formpad1 mt10">
     <div class="formleftpad">
     	<div class="formsubtitle">
        1.2 中文姓名(如有， 请用汉字填写)
        </div>
        <div class="formsubbox">
        <input type="checkbox" title="" name="nameInChineseCheck"  value="N/A" id="nameInChineseCheck" onClick="checkChange()"/>不适用 <br />
          <input type="text" name="nameInChinese" maxlength="50" value="" id="nameInChinese" class="inputtext" style="width:330px" data-validation-engine="validate[required,maxSize[50]]"/>
          <!--<span class="formFieldError">

         </span> -->
        </div>

     </div>

     <div class="helppad">
     <div class="helptext">
     请填写你的中文姓名(如有，请用汉字填写)。
	</div>
    </div>

     </div>



     <div class="formpad1 mt10">
     <div class="formleftpad">
     	<div class="formsubtitle">
        1.3 别名或曾用名
        </div>
        <div class="formsubbox">
        <input type="checkbox" name="formerNameCheck"  value="N/A" id="formerNameCheck" onClick="checkChange()"/>不适用<br />
          <input type="text" name="formerName" maxlength="50" value="" id="formerName" class="inputtext" style="width:380px" data-validation-engine="validate[required,maxSize[50]]"/>
          <!--<span class="formFieldError">

         </span>-->
        </div>

     </div>

     <div class="helppad">
     <div class="helptext">
     请填写你的别名或曾用名。
	</div>

        </div>
     </div>



     <div class="formpad1 mt10">
     <div class="formleftpad">
     	<div class="formsubtitle">
        1.4 性别
        </div>
       <div class="formcheck4">
        <p><input type="radio" data-validation-engine="validate[required] radio" data-prompt-position="centerRight:+200" name="gender" id="genderM"  value="M"/><label for="genderM">男</label>
		</p>
		<p><input type="radio" data-validation-engine="validate[required] radio" data-prompt-position="centerRight:+200" name="gender" id="genderF"  value="F"/><label for="genderF">女</label>
          </p>
         <br/>
        </div>
     </div>

     <div class="helppad">
     <div class="helptext">
     请选择你的性别。
	</div>
        </div>

     </div>


     <div class="formpad1 mt10">
     <div class="formleftpad" >
     	<div class="formsubtitle">
        1.5 申请人出生日期(格式为:yyyy-mm-dd)
        </div>
        <div class="formsubbox">
        <input type="text" name="dateOfBirth" maxlength="10" value="" id="dateOfBirth" class="inputtext" style="width:380px; " data-validation-engine="validate[required,custom[date]]"/>

        </div>

     </div>

     <div class="helppad">
     <div class="helptext">
     请填写你的出生日期。
	</div>
        </div>

     </div>


     <div class="formpad1 mt10">
     <div class="formleftpad">
     	<div class="formsubtitle">
        1.6 现有国籍
        </div>
        <div class="formsubbox">
        <input type="text" name="nationality" maxlength="120" value="" id="nationality" class="inputtext" style="width:380px" data-validation-engine="validate[required,maxSize[120]]"/>
        <!--<span class="formFieldError">

         </span>
        <br/><br/>
       是否在国籍国申请签证?<br />
       <div class="formcheck4">
          <p><input type="radio" data-validation-engine="validate[required] radio" data-prompt-position="centerRight:+180" name="applyNotCurrCountry" id="applyNotCurrCountryYes"  value="0"/><label for="applyNotCurrCountryYes">是</label>&nbsp&nbsp
		  </p>
		  <p><input type="radio" data-validation-engine="validate[required] radio" data-prompt-position="centerRight:+180" name="applyNotCurrCountry" id="applyNotCurrCountryNo"  value="1"/><label for="applyNotCurrCountryNo">否</label>
           </p></div>
          <br/>-->
          </div>
     </div>

     <div class="helppad">
     <div class="helptext">
     请填写你护照上的国籍。
	</div>
        </div>

     </div>


     <div class="formpad1 mt10">
     <div class="formleftpad">
     	<div class="formsubtitle">
        1.7 曾有国籍
        </div>
        <div class="formsubbox">
        <input type="checkbox" name="formerNationalityCheck"  value="N/A" id="formerNationalityCheck" onClick="checkChange()"/>不适用 <br />

          <input type="text" name="formerNationality" maxlength="120" value="" id="formerNationality" class="inputtext" style="width:380px" data-validation-engine="validate[required,maxSize[120]]"/>
          <!--<span class="formFieldError">

          </span>-->
        </div>
     </div>

     <div class="helppad">
     <div class="helptext">
     请你填写曾经具有的国籍。
	</div>
        </div>

     </div>

     <div class="formpad1 mt10">
     <div class="formleftpad">
     	<div class="formsubtitle">
        1.8出生地点（国家、省／市）
        </div>
         <div class="formsubbox">
        <div class="formcheck">
        国家<br />
        <input type="text" name="countryOfBirth" maxlength="120" value="" id="countryOfBirth" class="inputtext" style="width:380px" data-validation-engine="validate[required,maxSize[120]]"/>
        <!--<span class="formFieldError">

          </span>-->

        <br/>
        <!--
        <span id="chinaDiv" style="display: none">
        <br/>
      	<select name="cityOfBirth" id="cityOfBirth" style="width:120px;"></select>
      	label.application.form.text1101<input type="text" name="provinceOfBirth" maxlength="50" value="" id="provinceOfBirth" class="inputtext" style="width:200px" onBlur="this.className='inputtext_off';this.onmouseout=function(){this.className='inputtext'};" onFocus="this.className='inputtext_on';this.onmouseout=''"/><br />



      	label.application.form.text1102<input type="text" name="cityOfBirth" maxlength="50" value="" id="cityOfBirth" class="inputtext" style="width:200px" onBlur="this.className='inputtext_off';this.onmouseout=function(){this.className='inputtext'};" onFocus="this.className='inputtext_on';this.onmouseout=''"/><br />



      	</span> -->
      	<br/>
      	省/市<br />
        <input type="text" name="detailsOfBirth" maxlength="100" value="" id="detailsOfBirth" class="inputtext" style="width:380px" title="" data-validation-engine="validate[required,maxSize[100]]"/>
        <!--<span class="formFieldError">

          </span>-->
        <br />
        </div>
        </div>

     </div>

     <div class="helppad">
     <div class="helptext">
     请填写你出生地（国、省/州、市）的名称。
	</div>
        </div>

     </div>

     <div class="formpad1 mt10">
     <div class="formleftpad">
     	<div class="formsubtitle">
        1.9  身份证/公民证号码
        </div>
        <div class="formsubbox">
        <input type="checkbox" name="idNumberCheck"      value="N/A" id="idNumberCheck" onClick="checkChange()" />
        不适用 <br />
        <input type="text" name="idNumber" maxlength="50" value="" id="idNumber" class="inputtext" style="width:380px" data-validation-engine="validate[required,maxSize[50]]"/>
        <!--<span class="formFieldError">

          </span>-->
        </div>

     </div>

     <div class="helppad">
     <div class="helptext">
     请填写你在当地的身份证/公民证号码。
	</div>
        </div>

     </div>


     <div class="formpad1 mt10">
     <div class="formleftpad">
     	<div class="formsubtitle">
        1.10 护照/旅行证件种类
        </div>
        <div class="formsubbox">
     <div class="formcheck">
          <p><input type="radio" data-validation-engine="validate[required] radio" data-prompt-position="topRight:+160" name="passportType"   id="ApplicationApply_form2_passportTypeREG" value="REG"/><label for="ApplicationApply_form2_passportTypeREG">普通</label></p>
          <p><input type="radio" data-validation-engine="validate[required] radio" data-prompt-position="topRight:+160" name="passportType"   id="ApplicationApply_form2_passportTypeDIP" value="DIP"/><label for="ApplicationApply_form2_passportTypeDIP">外交</label></p>

		<p style="width:500px"><input type="radio" data-validation-engine="validate[required] radio" data-prompt-position="topRight:+160" name="passportType"   id="ApplicationApply_form2_passportTypeSRV" value="SRV"/><label for="ApplicationApply_form2_passportTypeSRV">公务、官员</label></p>
		<p style="width:500px"><input type="radio" data-validation-engine="validate[required] radio" data-prompt-position="topRight:+160" name="passportType"   id="ApplicationApply_form2_passportTypeOTH" value="OTH"/><label for="ApplicationApply_form2_passportTypeOTH">其它证件（请说明）</label>
      	<input type="text" name="passportTypeOther" maxlength="100" value="" id="passportTypeOther" class="inputtext" style="width:260px" data-validation-engine="validate[condRequired[ApplicationApply_form2_passportTypeOTH],maxSize[100]]"/></span>

         </p>
	  	</div>
     </div>
     </div>

     <div class="helppad">
     <div class="helptext">
     请选择你申请签证所持护照的种类；如持用非护照的旅行证件，另请详细说明。
	</div>
        </div>

     </div>


     <div class="formpad1 mt10">
     <div class="formleftpad">
     	<div class="formsubtitle">
        1.11 护照号码
        </div>
        <div class="formsubbox">
      <input type="text" name="passportNumber" maxlength="30" value="" id="passportNumber" class="inputtext" style="width:380px" data-validation-engine="validate[required,maxSize[30],custom[onlyLetterNumber]]"/>
     		<!--
     		<span class="formFieldError">

         	</span> -->
     </div>
     </div>

     <div class="helppad">
             <div class="helptext">
             请填写你申请签证所持护照的号码。
            </div>
        </div>

     </div>




      <div id="buttonside" class="mt10">
        <input type="button" class="btnblue1 f_r" value="下一步&gt;" onclick="nextForm(this.form);"/>
        <input type="button" class="btngreen1 f_l" value="保存" onclick="saveTemp(this.form);" />
      </div>
    </div>

      <!--
    <div id="formprompt">

      <input type="text" id="dateOfBirth" name="dateOfBirth" class="Wdate" onkeypress="WdatePicker({maxDate:'%y-%M-{%d-1}'})" onClick="WdatePicker({maxDate:'%y-%M-{%d-1}'})" value="" />
      <input type="button" value="label.application.common.button.exprot" onclick="expfile(this.form);" class="button_save"/>&nbsp;
      table cellpadding="0" cellspacing="0" class="idtable">
        <tr>
          <td width="100">EXPIRATION DATE:</td>
          <td>

          2017-01-08
          </td>
        </tr>
        <tr>
          <td>ESTIMATED BURDEN</td>
          <td>75 MIN</td>
        </tr>
      </table
      <div id="formdownload">
      <div class="textpadd">You may click the question mark behind every question for detail help or download the whole help document to learn how to fill the form.</div>
      <div align="center"><button class="btn_mouseout" onmouseover="this.className='btn_mouseover'"onmouseout="this.className='btn_mouseout'" title="Download Pdf" disabled="disabled">Download Pdf</button></div>
       </div>-->

       <!-- 原来的帮助
       <div id="helpdiv">
           <div id="titlehelp"><span class="orange">帮助</span>&nbsp;</div>
           <div id="helptext" class="textpadd">点击问号可以查看帮助详细信息!
           </div>

           <div id="buttonside"><input type="button"  class="button" onClick="MM_showHideLayers('helpdiv','','hide')" value="关闭"/></div>
       </div>

    </div>
    -->

    </form>





    </div><!-- contentbox780end -->
  </div>
</div>
    <div class="chamidboxbotttom"></div>
</div>
</body>
</html>