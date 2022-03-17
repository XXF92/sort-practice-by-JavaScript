
//生成随机顺序的数组 length数组长度
function create_arr(length){
	var random_array = new Array();
	for(var i = 0;i<length;i++){
		random_array.push(i);
	}
	//打乱顺序
	random_array.sort(()=>{return 0.5-Math.random()});
	return random_array;
}


//交换数组的两个位置的值
function swap(ind_1,ind_2,arr){
	let tmp = arr[ind_1];
	arr[ind_1] = arr[ind_2];
	arr[ind_2] = tmp;
	return arr;
}
//判断数组是否有序 正序
function arr_check_sort(arr){
	var flag = true;
	for(var i=0;i<arr.length-1;i++){
		if(arr[i]>arr[i+1]){
			flag = false;
			return flag;
		}
	}
	return flag;
}

// 调用不同的排序方法
function call_sort(func,length,...args){
	// let arr = Array.from(test);//不影响原数组
	let arr = create_arr(length);
	console.log("排序方法 " + func.name);
	console.log("原数组: "+arr.join(",") +" 长度: " +arr.length);

	//排序并计算所花时间
	let starTime = new Date(); 
	var res = func(arr,...args);
	let endTime = new Date(); 

	console.log("排序后: "+res.join(","));
	console.log("耗时: "+ (endTime.getTime() - starTime.getTime()));

	//检查是否有序
	if(arr_check_sort(res)){
		console.log("数组有序");
	}else{
		console.log("数组无序");
	}
}


var test = [15,4,83,8,3,17,44,25,66,1,38,55,1,5,50,38];
test = [82,85,86,89,87,86,83,82,85,86,89,83,81,88,84,80,81,1,100,77,66,54,0];
// var test = [15,18,6,6,20,18]
console.log("原数组 "+ test.join(",") +"长度 " + test.length);



// 基数排序 
function radix_sort(arr){
	//找数组的最大值
	let max_val = arr[0];
	for(var i = 0;i<arr.length;i++){
		if(arr[i] > max_val){
			max_val = arr[i];
		}
	}
	//数组最大的数是几位数
	var pos_num = 1;
	var tmp = max_val;
	while(tmp > 10){
		pos_num++;
		tmp = tmp/10;
	}

	//各个位进行计数排序
	var count_arr = new Array(); 
	var cou = 0;

	while(cou<pos_num){
		// 新建计数数组
		for(var i=0;i<10;i++){count_arr[i]=0;}//初始化计数为0
		//计数
		for(var i=0;i<arr.length;i++){
			var val = Math.floor(arr[i]/Math.pow(10,cou)) %10;
			// console.log("val= " +val)
			count_arr[val]++;
		}

		// 生成位置数组
		var index_arr = new Array();
		index_arr[0] = count_arr[0];
		for(var i=1;i<count_arr.length;i++){
			index_arr[i] = count_arr[i] + index_arr[i-1];
		}
		// console.log("count_arr "+count_arr.join(","));
		// 生成排序后数组
		var res_arr = new Array();
		for(var i=arr.length-1;i>=0;i--){
			res_arr[ index_arr[Math.floor(arr[i]/Math.pow(10,cou)) %10] -1 ] = arr[i];
			index_arr[ Math.floor(arr[i]/Math.pow(10,cou)) %10 ]--;
		}
		// console.log("res_arr "+res_arr.join(","));
		//把结果复制回原来的数组
		for(var i=0;i<res_arr.length;i++){
			arr[i] = res_arr[i];
		}

		cou++;
		// console.log("arr "+arr.join(","));

	}
	return arr;


}



//计数排序
function counting_sort(arr){
	//找数组的最大最小值
	let max_val = arr[0];
	let min_val = arr[0];
	for(var i = 0;i<arr.length;i++){
		if(arr[i] < min_val){
			min_val = arr[i];
		}
		if(arr[i] > max_val){
			max_val = arr[i];
		}
	}
	
	// 新建计数数组
	var count_arr = new Array();
	for(var i=0;i<=max_val-min_val;i++){
		count_arr[i] = 0;
	}
	//开始计数
	for(var i=0;i<arr.length;i++){
		count_arr[arr[i]-min_val]++;
	}

	// 生成位置数组
	var index_arr = new Array();
	index_arr[0] = count_arr[0];
	for(var i=1;i<count_arr.length;i++){
		index_arr[i] = count_arr[i] + index_arr[i-1];
	}
	//console.log("count_arr "+count_arr.join(","));

	//console.log("index_arr "+index_arr.join(","));


	//生成排序后结果数组
	var res_arr = new Array();

	//计数 不稳定写法
	// var j = 0;
	// for(var i=0;i<count_arr.length;i++){
	// 	while(count_arr[i] !=0){
	// 		res_arr[j] = i + min_val;
	// 		count_arr[i]--;
	// 		j++;
	// 	}
	// }

	//计数排序 稳定写法
	for(var i=arr.length-1;i>=0;i--){
		res_arr[index_arr[arr[i]-min_val] -1] = arr[i];
		index_arr[arr[i]-min_val]--;
	}

	return res_arr;

}



//快速排序 双轴快排
function quick_arr(arr,star,end){
	// console.log("原数组 "+arr.join(","));

	if(arr.length ==1){
		return ;
	}
	var pivot = arr[star];
	var left = star;
	var right = end;

	while(left < right){
		while(arr[right] > pivot && left < right){
			right--;
		}
		arr[left] = arr[right];


		while(arr[left] <= pivot && left < right){
			left++;
		}
		arr[right] = arr[left];
			
	
		if(left >= right){
			arr[left] = pivot;
		}
	}

	return left;

}


function quick_sort(arr,left,right){

	if(arr.length <= 1){
		return arr;
	}
	// console.log("arr="+ arr.join(","));

	if(left <right){
		mid = quick_arr(arr,left,right);
		//左边数组
		quick_sort(arr,left,mid-1);
		//右边数组
		// console.log("right_arr="+ right_arr.join(","));
		quick_sort(arr,mid+1,right);
		return arr;
	}else{
		return arr;
	}


}






//合并两个各自已经有序的数组
function merge_arr(arr,left,mid,right){

	if(arr.length<=1){
		return arr;
	}
	var tmp_arr = new Array();
	var i = left;
	var j = mid+1;
	var k = 0;
	//把小的项排前面
	while(i<=mid && j<=right){
		if(arr[i]<arr[j]){
			tmp_arr[k] = arr[i];
			i++;
			k++;
		}else{
			tmp_arr[k] = arr[j];
			j++;
			k++;
		}
	
	}
	//加入剩余的项
	while(i<=mid && j>=right){
		tmp_arr[k] = arr[i];
		i++;
		k++;
	}
	//加入剩余的项
	while(i>=mid && j<=right){
		tmp_arr[k] = arr[j];
		j++;
		k++;
	}
	for(var i = 0;i<tmp_arr.length;i++){
		arr[i+left] = tmp_arr[i]; 
	}

	// return arr;
	
}

//归并排序 递归 先拆分数组，然后在合并时排序
function merge_sort(arr,left,right){

	if(left<right){
		var sli = Math.floor((right+left)/2);
		//按照sli位置拆分arr数组
		merge_sort(arr,left,sli);//数组sli左边
		merge_sort(arr,sli+1,right);//数组sli右边
		//合并排序
		merge_arr(arr,left,sli,right);
		return arr;
		
	}else{
		//拆分到数组长度为1时，返回
		return arr;
	}
}




// 选择排序
function select_sort(arr){
	for (var i = 0; i < arr.length-1; i++) {
		for (var j = i+1;j<arr.length;j++) {
			if(arr[i]>arr[j]){
				arr = swap(i,j,arr);
			}
		}
	}
	return arr;
}

//冒泡排序
function bubble_sort(arr){
	//给冒泡加flag判断是否第一次遍历有进入到内层循环，如果没有进入循环说明原数组已经排好序，直接返回，此时时间复杂度为最好O(n)。
	var flag = true;
	for (var i = 0; i < arr.length; i++) {
		for (var j = 0;j<arr.length-i;j++) {
			flag = false;
			if(arr[j]>arr[j+1]){
				arr = swap(j,j+1,arr);
			}
		}
		if(flag){
			return;
		}
	}
	return arr;
}

//插入排序 有点像往前的冒泡
function insert_sort(arr){
	for (var i = 1; i < arr.length; i++) {
		for (var j = i;j>0 && arr[j]<arr[j-1];j--) {
			// if(arr[j]<arr[j-1]){
				arr = swap(j,j-1,arr);
			// }
		}
	}
	return arr;
}
//插入排序 改进
function insert_sort_2(arr){
	//从第二个数开始
	for (var i = 1; i < arr.length; i++) {
		//tmp 记录当前j角标的值，j往前遍历找到插入位置，期间遍历的值都往后移一位
		var tmp = arr[i];
		// 将arr分成有序区和无序区，初始有序区有一个元素。判断前一位的值与tmp的大小，判断是否结束循环
		for(var j =i;j>0 && arr[j-1]> tmp;j--){
			arr[j] = arr[j-1];
		}
		arr[j] = tmp;
		//console.log(arr.join(","))

	}
	return arr;
}

//插入排序 改进3 与上边insert_sort_2相同
function insert_sort_3(arr){
	for (var i = 1; i < arr.length; i++) {
		var tmp = arr[i];
		for(var j =i;j>0 ;j--){
			//结束循环
			if ( arr[j-1]< tmp){
				break;
			}
			arr[j] = arr[j-1];
		}
		arr[j] = tmp;
	}
	return arr;
}


//希尔排序 改进的插入排序
function shell_sort(arr){
	// 使用Knuth序列 h=3*h+1
	var h= 1;
	while(h <= arr.length/3){
		h = h*3 +1;
	}
	for(var gap = h; gap>0; gap = (gap-1)/3){
		//i从第一个gap开始 对后面每个数在其相隔gap的数组里排序
		for(var i =gap;i<arr.length;i++){
			var tmp = arr[i];
			//j>=gap 保证j-gap
			for(j = i; j>=gap && arr[j-gap]>tmp ;j-=gap){
				arr[j] = arr[j-gap];
			}
			arr[j] = tmp;
		}
	}
	return arr;
}



