# COUNTDOWN

Cut the crap, image first:

!https://github.com/harry-hxxxx/countdown/blob/master/doc/countdown.gif

Yeah my girlfriend wants a countdown timer to delay the course and punish her students, so...

All stuffs are in one single html page, without any lib, also no less, makes her could use it by dragging it into broswer directly without connecting to the internet.

Some reusable functions were included, such as tag-hidden-toggling, witch is a bothering job in javascript without AngularJS or other data-binding libs.here is the toggle function:

`
/*
*reusable function
*
*params:
*scope: tag that the scope want to toggle, please send <document> if you want to toggle in the whole page
*class_arr: array of class that want to toggle
*status_arr: 2d array, key: [status][index of class_arr], value: hidden or not for the class, 1 for show and 0 for hidden
*status: target status that want to change to
*
*1. define single time toggle function, add or remove hidden attribute of tags with that class name
*2. define reusable function array_contains_key to check if param status is in class_arr
*3. do loop, call single time toggle function sending class name one by one according to class_arr
*/
var toggle = function(scope, class_arr, status_arr, status){
	/*
	*single toggle function, toggle 1 class name each call
	*/
	var do_toggle = function(className, show) {
		tag_arr = scope.getElementsByClassName(className);
		for (var i = 0; i < tag_arr.length; i++){
				tag_arr[i].hidden = !show;
		}
	}
	/*
	*reusable function, to check if str is an index of an array
	*/
	var array_contains_key = function(arr, str){
		var b = false;
		for (var a in arr){
			if(a==str){b=true;}
		}
		return b;
	}
	if(class_arr.length>0 && class_arr.length==status_arr[status].length && array_contains_key(status_arr,status)){
		for (var i = 0; i < class_arr.length; i++){
			do_toggle(class_arr[i], status_arr[status][i]);
		}
	}
};
`

And below is an example to use the toggle function:

`class_arr = ['countdown-select', 'countdown-time', 'countdown-btn-run', 'countdown-btn-pause', 'countdown-btn-continue', 'countdown-btn-reset'];
status_arr = new Array();
status_arr['ready'] = [1,0,1,0,0,0];
status_arr['running'] = [0,1,0,1,0,1];
status_arr['pause'] = [0,1,0,0,1,1];
status_arr['stop'] = [0,1,0,0,0,1];
var countdown = document.getElementById("countdown");
toggle(countdown, class_arr, status_arr, 'ready');`
