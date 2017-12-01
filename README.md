# 天平称盐程序设计
 有一个天平,2克和7克砝码各一个。 若利用天平砝码将140克盐分成50,90克两份， 规定只能使用3次天平进行称量，有哪些方法？

<b>程序还太过于冗杂笨重，请求大神修改建议</b>
 
具体特别想优化的内容在float chenyan::f(float x, int fn){……}

1	代码

//有一个天平,2克和7克砝码各一个。利用天平砝码在将140克盐分成50,90克两份。若规定只能使用3次天平进行称量，有哪些方法？
#include <iostream>
//#include "h1.h" 
#include <string>
using namespace std;

class chenyan{
private:
	//变量定义
	float start = 0, a1 = 0, a2 = 0, b1 = 0, b2 = 0, c1 = 0, c2 = 0;
	float aa2 = 0, bb2 = 0, cc2 = 0;//分量暂存器
	int n;   //记录第几步
	int i, j, k; //记录应该使用的方法
	int shu = 0;//记录可行的方法第几种
	float A1[10];
	float A2[10];
	float A3[10];
public:
	//函数声明
	chenyan(float xx){ start = xx; };	//构造对象
	void func();        //功能实现
	float f(float x, int xx);	//具体方法实现
	void data(float x, float y, float y2, float nn, float eha2, float ehb2, float f, float  _f, float _a2, float _b2);
	void show(float x, float y, float y2, float nn, float eha2, float ehb2, float f, float  _f, float _a2, float _b2);
	//【x】,【y】,【nn：1平移、2平分】，【eha2】，【ehb2】,【f】，【_f】，【_a2】,【_b2】
};

void chenyan::func(){
	for (i = 0; i < 13; i++){	//将盐start分为a1,a2
		n = 1;
		a1 = f(start, i);
		aa2 = a2;	//保存a2的原始值以便下层循环使用,因为a2在f()中会被不断改变

		for (j = 0; j < 30; j++){		//将盐a1分为b1,b2
			n = 2;
			a2 = aa2;//k循环结束，恢复变量值以便j循环使用
			b1 = f(a1, j);
			bb2 = b2;	//同上

			for (k = 0; k < 64; k++){			//将盐b1分为c1,c2
				n = 3;
				c1 = f(b1, k);

				if (c1 == 50 || c1 == 90){
					shu++;
					cout << "*****第【" << shu << "】种方法：*****" << endl;
					cout << start << " -> " << a1 << " -> " << b1 << " -> " << c1
						<< "  此时，i= " << i << "，j= " << j << "，k= " << k << endl;
					cout << "过程详解：" << endl;
					n = 1;	show(A1[0], A1[1], A1[2], A1[3], A1[4], A1[5], A1[6], A1[7], A1[8], A1[9]);
					n = 2;	show(A2[0], A2[1], A2[2], A2[3], A2[4], A2[5], A2[6], A2[7], A2[8], A2[9]);
					n = 3;	show(A3[0], A3[1], A3[2], A3[3], A3[4], A3[5], A3[6], A3[7], A3[8], A3[9]);
					cout << endl << endl;

				};

			}
		}
	}
}

void chenyan::data(float x, float y, float y2, float nn, float eha2, float ehb2, float f, float  _f, float _a2, float _b2){
	if (n == 1){
		A1[0] = x; A1[1] = y; A1[2] = y2; A1[3] = nn;  A1[4] = eha2; A1[5] = ehb2; A1[6] = f; A1[7] = _f; A1[8] = _a2; A1[9] = _b2;
	};
	if (n == 2){
		A2[0] = x; A2[1] = y; A2[2] = y2; A2[3] = nn;  A2[4] = eha2; A2[5] = ehb2; A2[6] = f; A2[7] = _f; A2[8] = _a2; A2[9] = _b2;
	};
	if (n == 3){
		A3[0] = x; A3[1] = y; A3[2] = y2; A3[3] = nn;  A3[4] = eha2; A3[5] = ehb2; A3[6] = f; A3[7] = _f; A3[8] = _a2; A3[9] = _b2;
	};
};

void chenyan::show(float x, float y, float y2, float nn, float eha2, float ehb2, float f, float  _f, float _a2, float _b2){
	cout << "第" << n << "步: " << endl;
	if (f > 0) { cout << "<将砝码" << f << "g放天平左侧>	"; };
	if (_f > 0){ cout << "<将砝码" << _f << "g放天平右侧>	"; };
	if (nn == 1){
		if (_a2 > 0){ cout << "<将分量【a2】:" << _a2 << "g放天平右侧>	"; };
		if (_b2 > 0){ cout << "<将分量【b2】:" << _b2 << "g放天平右侧>	"; };
		cout << endl << "从" << x << "g沙堆中取出" << y2 << "g沙子到天平左侧";
		if (n == 1){ cout << "(作为【a2】)，" << "剩下沙堆:" << x - y2 << "g(作为【a1】)"; };
		if (n == 2){ cout << "(作为【b2】)，" << "剩下沙堆:" << x - y2 << "g(作为【b1】)"; };
		if (n == 3){ cout << "(作为【c2】)，" << "剩下沙堆:" << x - y2 << "g(作为【c1】)"; };
		cout << endl;
	};
	if (nn == 2){
		cout << endl << "从" << x << "g沙堆中取出" << y - eha2 - ehb2 << "g沙子到天平左侧";
		if (n == 1){ cout << "(作为【a1】)，" << x - y + eha2 + ehb2 << "g到天平右侧(作为【a2】)"; };
		if (n == 2){ cout << "(作为【b1】)，" << x - y + eha2 + ehb2 << "g到天平右侧(作为【b2】)"; };
		if (n == 3){ cout << "(作为【c1】)，" << x - y + eha2 + ehb2 << "g到天平右侧(作为【c2】)"; };
		cout << endl;
	};

	if (eha2 > 0){
		cout << "将分量【a2】:" << eha2 << "g与所得沙堆合并得" << y;
		if (n == 2){ cout << "g (作新的【b1】)"; }
		else{ cout << "g (作新的【c1】)"; }
	}
	if (ehb2 > 0){ cout << "将分量【b2】:" << ehb2 << "g与所得沙堆合并得" << y << "g (作新的【c1】)"; };
	cout << endl;
}


float chenyan::f(float x, int fn){
	//jj = "【x平分为2份】"; jj = "【x加上砝码2g，平分为2份，取无砝码那份】";jj = "【x加上砝码2g，平分为2份，取有砝码那份】"; 
	float y, y2;//返回的结果
	switch (fn) {
	case 0:		y = x - 2; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 0, 2, 0, 0);		 break;
	case 1:		y = x - 5; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 2, 7, 0, 0);		 break;
	case 2:		y = x - 7; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 0, 7, 0, 0);		 break;
	case 3:		y = x - 9; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 0, 9, 0, 0);		 break;
	case 4:		y = (x + 0) / 2; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 2, 0, 0, 0, 0, 0, 0);		 break;
	case 5:		y = (x + 2) / 2; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 2, 0, 0, 0, 2, 0, 0);		 break;
	case 6:		y = (x + 2) / 2 - 2; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 2, 0, 0, 2, 0, 0, 0);		 break;
	case 7:		y = (x + 7) / 2; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 2, 0, 0, 0, 7, 0, 0);		 break;
	case 8:		y = (x + 7) / 2 - 7; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 2, 0, 0, 7, 0, 0, 0);		 break;
	case 9:		y = (x + 9) / 2; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 2, 0, 0, 0, 9, 0, 0);		 break;
	case 10:		y = (x + 9) / 2 - 2; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 2, 0, 0, 2, 7, 0, 0);		 break;
	case 11:		y = (x + 9) / 2 - 7; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 2, 0, 0, 7, 2, 0, 0);		 break;
	case 12:		y = (x + 9) / 2 - 9; 	if (n == 1){ a2 = start - y; y2 = a2; };	if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 2, 0, 0, 9, 0, 0, 0);		 break;
	case 13:		y = x - 2 - aa2; 		if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 0, 2, aa2, 0);		 break;
	case 14:		y = x - 5 - aa2; 		if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 2, 7, aa2, 0);		 break;
	case 15:		y = x - 7 - aa2; 		if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 0, 7, aa2, 0);		 break;
	case 16:		y = x - 9 - aa2; 		if (n == 2){ b2 = a1 - y;	y2 = b2; };	if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 0, 9, aa2, 0);		 break;
	case 17:		y = x - 2 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 1, aa2, 0, 0, 2, 0, 0);		 break;
	case 18:		y = x - 5 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 1, aa2, 0, 2, 7, 0, 0);		 break;
	case 19:		y = x - 7 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 1, aa2, 0, 0, 7, 0, 0);		 break;
	case 20:		y = x - 9 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 1, aa2, 0, 0, 9, 0, 0);		 break;
	case 21:		y = (x + 0) / 2 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 2, aa2, 0, 0, 0, 0, 0);		 break;
	case 22:		y = (x + 2) / 2 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 2, aa2, 0, 0, 2, 0, 0);		 break;
	case 23:		y = (x + 2) / 2 - 2 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 2, aa2, 0, 2, 0, 0, 0);		 break;
	case 24:		y = (x + 7) / 2 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 2, aa2, 0, 0, 7, 0, 0);		 break;
	case 25:		y = (x + 7) / 2 - 7 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 2, aa2, 0, 7, 0, 0, 0);		 break;
	case 26:		y = (x + 9) / 2 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 2, aa2, 0, 0, 9, 0, 0);		 break;
	case 27:		y = (x + 9) / 2 - 2 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 2, aa2, 0, 2, 7, 0, 0);		 break;
	case 28:		y = (x + 9) / 2 - 7 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 2, aa2, 0, 7, 2, 0, 0);		 break;
	case 29:		y = (x + 9) / 2 - 9 + aa2; 		if (n == 2){ b2 = a1 - (y - a2);	y2 = b2; };	if (n == 3){ c2 = b1 - (y - a2);	y2 = c2; };	a2 = 0;	data(x, y, y2, 2, aa2, 0, 9, 0, 0, 0);		 break;
	case 30:		y = x - 2 - bb2; 					if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 0, 2, 0, bb2);		 break;
	case 31:		y = x - 5 - bb2; 					if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 2, 7, 0, bb2);		 break;
	case 32:		y = x - 7 - bb2; 					if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 0, 7, 0, bb2);		 break;
	case 33:		y = x - 9 - bb2; 					if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 0, 9, 0, bb2);		 break;
	case 34:		y = x - 2 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 1, 0, bb2, 0, 2, 0, 0);		 break;
	case 35:		y = x - 5 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 1, 0, bb2, 2, 7, 0, 0);		 break;
	case 36:		y = x - 7 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 1, 0, bb2, 0, 7, 0, 0);		 break;
	case 37:		y = x - 9 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 1, 0, bb2, 0, 9, 0, 0);		 break;
	case 38:		y = (x + 0) / 2 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 2, 0, bb2, 0, 0, 0, 0);		 break;
	case 39:		y = (x + 2) / 2 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 2, 0, bb2, 0, 2, 0, 0);		 break;
	case 40:		y = (x + 2) / 2 - 2 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 2, 0, bb2, 2, 0, 0, 0);		 break;
	case 41:		y = (x + 7) / 2 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 2, 0, bb2, 0, 7, 0, 0);		 break;
	case 42:		y = (x + 7) / 2 - 7 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 2, 0, bb2, 7, 0, 0, 0);		 break;
	case 43:		y = (x + 9) / 2 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 2, 0, bb2, 0, 9, 0, 0);		 break;
	case 44:		y = (x + 9) / 2 - 2 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 2, 0, bb2, 2, 7, 0, 0);		 break;
	case 45:		y = (x + 9) / 2 - 7 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 2, 0, bb2, 7, 2, 0, 0);		 break;
	case 46:		y = (x + 9) / 2 - 9 + bb2;					if (n == 3){ c2 = b1 - (y - b2);	y2 = c2; };		data(x, y, y2, 2, 0, bb2, 9, 0, 0, 0);		 break;
	case 47:	if (a2>0){ y = x - 2 - aa2 - bb2; 					if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 0, 2, aa2, bb2); }
				else{ y = -10000; };	 break;
	case 48:	if (a2>0){ y = x - 5 - aa2 - bb2; 					if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 2, 7, aa2, bb2); }
				else{ y = -10000; };	 break;
	case 49:	if (a2>0){ y = x - 7 - aa2 - bb2; 					if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 0, 7, aa2, bb2); }
				else{ y = -10000; };	 break;
	case 50:	if (a2>0){ y = x - 9 - aa2 - bb2; 					if (n == 3){ c2 = b1 - y;	y2 = c2; };		data(x, y, y2, 1, 0, 0, 0, 9, aa2, bb2); }
				else{ y = -10000; };	 break;
	case 51:	if (a2>0){ y = x - 2 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 1, aa2, bb2, 0, 2, 0, 0); }
				else{ y = -10000; };	 break;
	case 52:	if (a2>0){ y = x - 5 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 1, aa2, bb2, 2, 7, 0, 0); }
				else{ y = -10000; };	 break;
	case 53:	if (a2>0){ y = x - 7 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 1, aa2, bb2, 0, 7, 0, 0); }
				else{ y = -10000; };	 break;
	case 54:	if (a2>0){ y = x - 9 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 1, aa2, bb2, 0, 9, 0, 0); }
				else{ y = -10000; };	 break;
	case 55:	if (a2>0){ y = (x + 0) / 2 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 2, aa2, bb2, 0, 0, 0, 0); }
				else{ y = -10000; };	 break;
	case 56:	if (a2>0){ y = (x + 2) / 2 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 2, aa2, bb2, 0, 2, 0, 0); }
				else{ y = -10000; };	 break;
	case 57:	if (a2>0){ y = (x + 2) / 2 - 2 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 2, aa2, bb2, 2, 0, 0, 0); }
				else{ y = -10000; };	 break;
	case 58:	if (a2>0){ y = (x + 7) / 2 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 2, aa2, bb2, 0, 7, 0, 0); }
				else{ y = -10000; };	 break;
	case 59:	if (a2>0){ y = (x + 7) / 2 - 7 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 2, aa2, bb2, 7, 0, 0, 0); }
				else{ y = -10000; };	 break;
	case 60:	if (a2>0){ y = (x + 9) / 2 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 2, aa2, bb2, 0, 9, 0, 0); }
				else{ y = -10000; };	 break;
	case 61:	if (a2>0){ y = (x + 9) / 2 - 2 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 2, aa2, bb2, 2, 7, 0, 0); }
				else{ y = -10000; };	 break;
	case 62:	if (a2>0){ y = (x + 9) / 2 - 7 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 2, aa2, bb2, 7, 2, 0, 0); }
				else{ y = -10000; };	 break;
	case 63:	if (a2>0){ y = (x + 9) / 2 - 9 + aa2 + bb2;  					if (n == 3){ c2 = b1 - (y - a2 - b2);	y2 = c2; };		data(x, y, y2, 2, aa2, bb2, 9, 0, 0, 0); }
				else{ y = -10000; };	 break;
	};

	return y;
}



int main(){
	cout << "有一个天平,2克和7克砝码各一个。利用天平砝码在将140克盐分成50,90克两份。若规定只能使用3次天平进行称量，有哪些方法？" << endl;
	chenyan f1(140);
	f1.func();
	return 0;
}
2	结果

有一个天平,2克和7克砝码各一个。利用天平砝码在将140克盐分成50,90克两份。若规定只能使用3次天平进行称量，有哪些方法？
*****第【1】种方法：*****
140 -> 135 -> 64 -> 50  此时，i= 1，j= 8，k= 16
过程详解：
第1步:
<将砝码2g放天平左侧>    <将砝码7g放天平右侧>
从140g沙堆中取出5g沙子到天平左侧(作为【a2】)，剩下沙堆:135g(作为【a1】)

第2步:
<将砝码7g放天平左侧>
从135g沙堆中取出64g沙子到天平左侧(作为【b1】)，71g到天平右侧(作为【b2】)

第3步:
<将砝码9g放天平右侧>    <将分量【a2】:5g放天平右侧>
从64g沙堆中取出14g沙子到天平左侧(作为【c2】)，剩下沙堆:50g(作为【c1】)



*****第【2】种方法：*****
140 -> 133 -> 64 -> 50  此时，i= 2，j= 11，k= 15
过程详解：
第1步:
<将砝码7g放天平右侧>
从140g沙堆中取出7g沙子到天平左侧(作为【a2】)，剩下沙堆:133g(作为【a1】)

第2步:
<将砝码7g放天平左侧>    <将砝码2g放天平右侧>
从133g沙堆中取出64g沙子到天平左侧(作为【b1】)，69g到天平右侧(作为【b2】)

第3步:
<将砝码7g放天平右侧>    <将分量【a2】:7g放天平右侧>
从64g沙堆中取出14g沙子到天平左侧(作为【c2】)，剩下沙堆:50g(作为【c1】)



*****第【3】种方法：*****
140 -> 133 -> 62 -> 50  此时，i= 2，j= 12，k= 14
过程详解：
第1步:
<将砝码7g放天平右侧>
从140g沙堆中取出7g沙子到天平左侧(作为【a2】)，剩下沙堆:133g(作为【a1】)

第2步:
<将砝码9g放天平左侧>
从133g沙堆中取出62g沙子到天平左侧(作为【b1】)，71g到天平右侧(作为【b2】)

第3步:
<将砝码2g放天平左侧>    <将砝码7g放天平右侧>    <将分量【a2】:7g放天平右侧>
从62g沙堆中取出12g沙子到天平左侧(作为【c2】)，剩下沙堆:50g(作为【c1】)



*****第【4】种方法：*****
140 -> 133 -> 77 -> 50  此时，i= 2，j= 24，k= 26
过程详解：
第1步:
<将砝码7g放天平右侧>
从140g沙堆中取出7g沙子到天平左侧(作为【a2】)，剩下沙堆:133g(作为【a1】)

第2步:
<将砝码7g放天平右侧>
从133g沙堆中取出70g沙子到天平左侧(作为【b1】)，63g到天平右侧(作为【b2】)
将分量【a2】:7g与所得沙堆合并得77g (作新的【b1】)
第3步:
<将砝码9g放天平右侧>
从77g沙堆中取出43g沙子到天平左侧(作为【c1】)，34g到天平右侧(作为【c2】)
将分量【a2】:7g与所得沙堆合并得50g (作新的【c1】)


*****第【5】种方法：*****
140 -> 131 -> 68 -> 50  此时，i= 3，j= 10，k= 16
过程详解：
第1步:
<将砝码9g放天平右侧>
从140g沙堆中取出9g沙子到天平左侧(作为【a2】)，剩下沙堆:131g(作为【a1】)

第2步:
<将砝码2g放天平左侧>    <将砝码7g放天平右侧>
从131g沙堆中取出68g沙子到天平左侧(作为【b1】)，63g到天平右侧(作为【b2】)

第3步:
<将砝码9g放天平右侧>    <将分量【a2】:9g放天平右侧>
从68g沙堆中取出18g沙子到天平左侧(作为【c2】)，剩下沙堆:50g(作为【c1】)



*****第【6】种方法：*****
140 -> 131 -> 61 -> 50  此时，i= 3，j= 12，k= 13
过程详解：
第1步:
<将砝码9g放天平右侧>
从140g沙堆中取出9g沙子到天平左侧(作为【a2】)，剩下沙堆:131g(作为【a1】)

第2步:
<将砝码9g放天平左侧>
从131g沙堆中取出61g沙子到天平左侧(作为【b1】)，70g到天平右侧(作为【b2】)

第3步:
<将砝码2g放天平右侧>    <将分量【a2】:9g放天平右侧>
从61g沙堆中取出11g沙子到天平左侧(作为【c2】)，剩下沙堆:50g(作为【c1】)



*****第【7】种方法：*****
140 -> 131 -> 115 -> 90  此时，i= 3，j= 15，k= 33
过程详解：
第1步:
<将砝码9g放天平右侧>
从140g沙堆中取出9g沙子到天平左侧(作为【a2】)，剩下沙堆:131g(作为【a1】)

第2步:
<将砝码7g放天平右侧>    <将分量【a2】:9g放天平右侧>
从131g沙堆中取出16g沙子到天平左侧(作为【b2】)，剩下沙堆:115g(作为【b1】)

第3步:
<将砝码9g放天平右侧>    <将分量【b2】:16g放天平右侧>
从115g沙堆中取出25g沙子到天平左侧(作为【c2】)，剩下沙堆:90g(作为【c1】)



*****第【8】种方法：*****
140 -> 131 -> 113 -> 90  此时，i= 3，j= 16，k= 31
过程详解：
第1步:
<将砝码9g放天平右侧>
从140g沙堆中取出9g沙子到天平左侧(作为【a2】)，剩下沙堆:131g(作为【a1】)

第2步:
<将砝码9g放天平右侧>    <将分量【a2】:9g放天平右侧>
从131g沙堆中取出18g沙子到天平左侧(作为【b2】)，剩下沙堆:113g(作为【b1】)

第3步:
<将砝码2g放天平左侧>    <将砝码7g放天平右侧>    <将分量【b2】:18g放天平右侧>
从113g沙堆中取出23g沙子到天平左侧(作为【c2】)，剩下沙堆:90g(作为【c1】)



*****第【9】种方法：*****
140 -> 131 -> 77 -> 50  此时，i= 3，j= 27，k= 27
过程详解：
第1步:
<将砝码9g放天平右侧>
从140g沙堆中取出9g沙子到天平左侧(作为【a2】)，剩下沙堆:131g(作为【a1】)

第2步:
<将砝码2g放天平左侧>    <将砝码7g放天平右侧>
从131g沙堆中取出68g沙子到天平左侧(作为【b1】)，63g到天平右侧(作为【b2】)
将分量【a2】:9g与所得沙堆合并得77g (作新的【b1】)
第3步:
<将砝码2g放天平左侧>    <将砝码7g放天平右侧>
从77g沙堆中取出41g沙子到天平左侧(作为【c1】)，36g到天平右侧(作为【c2】)
将分量【a2】:9g与所得沙堆合并得50g (作新的【c1】)


*****第【10】种方法：*****
140 -> 70 -> 61 -> 50  此时，i= 4，j= 3，k= 30
过程详解：
第1步:

从140g沙堆中取出70g沙子到天平左侧(作为【a1】)，70g到天平右侧(作为【a2】)

第2步:
<将砝码9g放天平右侧>
从70g沙堆中取出9g沙子到天平左侧(作为【b2】)，剩下沙堆:61g(作为【b1】)

第3步:
<将砝码2g放天平右侧>    <将分量【b2】:9g放天平右侧>
从61g沙堆中取出11g沙子到天平左侧(作为【c2】)，剩下沙堆:50g(作为【c1】)



*****第【11】种方法：*****
140 -> 70 -> 35 -> 90  此时，i= 4，j= 4，k= 27
过程详解：
第1步:

从140g沙堆中取出70g沙子到天平左侧(作为【a1】)，70g到天平右侧(作为【a2】)

第2步:

从70g沙堆中取出35g沙子到天平左侧(作为【b1】)，35g到天平右侧(作为【b2】)

第3步:
<将砝码2g放天平左侧>    <将砝码7g放天平右侧>
从35g沙堆中取出20g沙子到天平左侧(作为【c1】)，15g到天平右侧(作为【c2】)
将分量【a2】:70g与所得沙堆合并得90g (作新的【c1】)


*****第【12】种方法：*****
140 -> 70 -> 35 -> 50  此时，i= 4，j= 4，k= 45
过程详解：
第1步:

从140g沙堆中取出70g沙子到天平左侧(作为【a1】)，70g到天平右侧(作为【a2】)

第2步:

从70g沙堆中取出35g沙子到天平左侧(作为【b1】)，35g到天平右侧(作为【b2】)

第3步:
<将砝码7g放天平左侧>    <将砝码2g放天平右侧>
从35g沙堆中取出15g沙子到天平左侧(作为【c1】)，20g到天平右侧(作为【c2】)
将分量【b2】:35g与所得沙堆合并得50g (作新的【c1】)


*****第【13】种方法：*****
140 -> 70 -> 105 -> 50  此时，i= 4，j= 21，k= 11
过程详解：
第1步:

从140g沙堆中取出70g沙子到天平左侧(作为【a1】)，70g到天平右侧(作为【a2】)

第2步:

从70g沙堆中取出35g沙子到天平左侧(作为【b1】)，35g到天平右侧(作为【b2】)
将分量【a2】:70g与所得沙堆合并得105g (作新的【b1】)
第3步:
<将砝码7g放天平左侧>    <将砝码2g放天平右侧>
从105g沙堆中取出50g沙子到天平左侧(作为【c1】)，55g到天平右侧(作为【c2】)



*****第【14】种方法：*****
140 -> 70 -> 105 -> 90  此时，i= 4，j= 21，k= 44
过程详解：
第1步:

从140g沙堆中取出70g沙子到天平左侧(作为【a1】)，70g到天平右侧(作为【a2】)

第2步:

从70g沙堆中取出35g沙子到天平左侧(作为【b1】)，35g到天平右侧(作为【b2】)
将分量【a2】:70g与所得沙堆合并得105g (作新的【b1】)
第3步:
<将砝码2g放天平左侧>    <将砝码7g放天平右侧>
从105g沙堆中取出55g沙子到天平左侧(作为【c1】)，50g到天平右侧(作为【c2】)
将分量【b2】:35g与所得沙堆合并得90g (作新的【c1】)


*****第【15】种方法：*****
140 -> 71 -> 64 -> 50  此时，i= 5，j= 2，k= 32
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平右侧>
从71g沙堆中取出7g沙子到天平左侧(作为【b2】)，剩下沙堆:64g(作为【b1】)

第3步:
<将砝码7g放天平右侧>    <将分量【b2】:7g放天平右侧>
从64g沙堆中取出14g沙子到天平左侧(作为【c2】)，剩下沙堆:50g(作为【c1】)



*****第【16】种方法：*****
140 -> 71 -> 40 -> 90  此时，i= 5，j= 9，k= 22
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码9g放天平右侧>
从71g沙堆中取出40g沙子到天平左侧(作为【b1】)，31g到天平右侧(作为【b2】)

第3步:
<将砝码2g放天平右侧>
从40g沙堆中取出21g沙子到天平左侧(作为【c1】)，19g到天平右侧(作为【c2】)
将分量【a2】:69g与所得沙堆合并得90g (作新的【c1】)


*****第【17】种方法：*****
140 -> 71 -> 40 -> 50  此时，i= 5，j= 9，k= 40
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码9g放天平右侧>
从71g沙堆中取出40g沙子到天平左侧(作为【b1】)，31g到天平右侧(作为【b2】)

第3步:
<将砝码2g放天平左侧>
从40g沙堆中取出19g沙子到天平左侧(作为【c1】)，21g到天平右侧(作为【c2】)
将分量【b2】:31g与所得沙堆合并得50g (作新的【c1】)


*****第【18】种方法：*****
140 -> 71 -> 33 -> 90  此时，i= 5，j= 11，k= 26
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平左侧>    <将砝码2g放天平右侧>
从71g沙堆中取出33g沙子到天平左侧(作为【b1】)，38g到天平右侧(作为【b2】)

第3步:
<将砝码9g放天平右侧>
从33g沙堆中取出21g沙子到天平左侧(作为【c1】)，12g到天平右侧(作为【c2】)
将分量【a2】:69g与所得沙堆合并得90g (作新的【c1】)


*****第【19】种方法：*****
140 -> 71 -> 33 -> 50  此时，i= 5，j= 11，k= 46
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平左侧>    <将砝码2g放天平右侧>
从71g沙堆中取出33g沙子到天平左侧(作为【b1】)，38g到天平右侧(作为【b2】)

第3步:
<将砝码9g放天平左侧>
从33g沙堆中取出12g沙子到天平左侧(作为【c1】)，21g到天平右侧(作为【c2】)
将分量【b2】:38g与所得沙堆合并得50g (作新的【c1】)


*****第【20】种方法：*****
140 -> 71 -> 109 -> 50  此时，i= 5，j= 26，k= 12
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码9g放天平右侧>
从71g沙堆中取出40g沙子到天平左侧(作为【b1】)，31g到天平右侧(作为【b2】)
将分量【a2】:69g与所得沙堆合并得109g (作新的【b1】)
第3步:
<将砝码9g放天平左侧>
从109g沙堆中取出50g沙子到天平左侧(作为【c1】)，59g到天平右侧(作为【c2】)



*****第【21】种方法：*****
140 -> 71 -> 109 -> 90  此时，i= 5，j= 26，k= 43
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码9g放天平右侧>
从71g沙堆中取出40g沙子到天平左侧(作为【b1】)，31g到天平右侧(作为【b2】)
将分量【a2】:69g与所得沙堆合并得109g (作新的【b1】)
第3步:
<将砝码9g放天平右侧>
从109g沙堆中取出59g沙子到天平左侧(作为【c1】)，50g到天平右侧(作为【c2】)
将分量【b2】:31g与所得沙堆合并得90g (作新的【c1】)


*****第【22】种方法：*****
140 -> 71 -> 107 -> 50  此时，i= 5，j= 27，k= 8
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码2g放天平左侧>    <将砝码7g放天平右侧>
从71g沙堆中取出38g沙子到天平左侧(作为【b1】)，33g到天平右侧(作为【b2】)
将分量【a2】:69g与所得沙堆合并得107g (作新的【b1】)
第3步:
<将砝码7g放天平左侧>
从107g沙堆中取出50g沙子到天平左侧(作为【c1】)，57g到天平右侧(作为【c2】)



*****第【23】种方法：*****
140 -> 71 -> 107 -> 90  此时，i= 5，j= 27，k= 41
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码2g放天平左侧>    <将砝码7g放天平右侧>
从71g沙堆中取出38g沙子到天平左侧(作为【b1】)，33g到天平右侧(作为【b2】)
将分量【a2】:69g与所得沙堆合并得107g (作新的【b1】)
第3步:
<将砝码7g放天平右侧>
从107g沙堆中取出57g沙子到天平左侧(作为【c1】)，50g到天平右侧(作为【c2】)
将分量【b2】:33g与所得沙堆合并得90g (作新的【c1】)


*****第【24】种方法：*****
140 -> 71 -> 102 -> 50  此时，i= 5，j= 28，k= 6
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平左侧>    <将砝码2g放天平右侧>
从71g沙堆中取出33g沙子到天平左侧(作为【b1】)，38g到天平右侧(作为【b2】)
将分量【a2】:69g与所得沙堆合并得102g (作新的【b1】)
第3步:
<将砝码2g放天平左侧>
从102g沙堆中取出50g沙子到天平左侧(作为【c1】)，52g到天平右侧(作为【c2】)



*****第【25】种方法：*****
140 -> 71 -> 102 -> 90  此时，i= 5，j= 28，k= 39
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平左侧>    <将砝码2g放天平右侧>
从71g沙堆中取出33g沙子到天平左侧(作为【b1】)，38g到天平右侧(作为【b2】)
将分量【a2】:69g与所得沙堆合并得102g (作新的【b1】)
第3步:
<将砝码2g放天平右侧>
从102g沙堆中取出52g沙子到天平左侧(作为【c1】)，50g到天平右侧(作为【c2】)
将分量【b2】:38g与所得沙堆合并得90g (作新的【c1】)


*****第【26】种方法：*****
140 -> 71 -> 100 -> 50  此时，i= 5，j= 29，k= 4
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码9g放天平左侧>
从71g沙堆中取出31g沙子到天平左侧(作为【b1】)，40g到天平右侧(作为【b2】)
将分量【a2】:69g与所得沙堆合并得100g (作新的【b1】)
第3步:

从100g沙堆中取出50g沙子到天平左侧(作为【c1】)，50g到天平右侧(作为【c2】)



*****第【27】种方法：*****
140 -> 71 -> 100 -> 90  此时，i= 5，j= 29，k= 38
过程详解：
第1步:
<将砝码2g放天平右侧>
从140g沙堆中取出71g沙子到天平左侧(作为【a1】)，69g到天平右侧(作为【a2】)

第2步:
<将砝码9g放天平左侧>
从71g沙堆中取出31g沙子到天平左侧(作为【b1】)，40g到天平右侧(作为【b2】)
将分量【a2】:69g与所得沙堆合并得100g (作新的【b1】)
第3步:

从100g沙堆中取出50g沙子到天平左侧(作为【c1】)，50g到天平右侧(作为【c2】)
将分量【b2】:40g与所得沙堆合并得90g (作新的【c1】)


*****第【28】种方法：*****
140 -> 69 -> 64 -> 50  此时，i= 6，j= 1，k= 33
过程详解：
第1步:
<将砝码2g放天平左侧>
从140g沙堆中取出69g沙子到天平左侧(作为【a1】)，71g到天平右侧(作为【a2】)

第2步:
<将砝码2g放天平左侧>    <将砝码7g放天平右侧>
从69g沙堆中取出5g沙子到天平左侧(作为【b2】)，剩下沙堆:64g(作为【b1】)

第3步:
<将砝码9g放天平右侧>    <将分量【b2】:5g放天平右侧>
从64g沙堆中取出14g沙子到天平左侧(作为【c2】)，剩下沙堆:50g(作为【c1】)



*****第【29】种方法：*****
140 -> 69 -> 62 -> 50  此时，i= 6，j= 2，k= 31
过程详解：
第1步:
<将砝码2g放天平左侧>
从140g沙堆中取出69g沙子到天平左侧(作为【a1】)，71g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平右侧>
从69g沙堆中取出7g沙子到天平左侧(作为【b2】)，剩下沙堆:62g(作为【b1】)

第3步:
<将砝码2g放天平左侧>    <将砝码7g放天平右侧>    <将分量【b2】:7g放天平右侧>
从62g沙堆中取出12g沙子到天平左侧(作为【c2】)，剩下沙堆:50g(作为【c1】)



*****第【30】种方法：*****
140 -> 69 -> 38 -> 90  此时，i= 6，j= 7，k= 21
过程详解：
第1步:
<将砝码2g放天平左侧>
从140g沙堆中取出69g沙子到天平左侧(作为【a1】)，71g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平右侧>
从69g沙堆中取出38g沙子到天平左侧(作为【b1】)，31g到天平右侧(作为【b2】)

第3步:

从38g沙堆中取出19g沙子到天平左侧(作为【c1】)，19g到天平右侧(作为【c2】)
将分量【a2】:71g与所得沙堆合并得90g (作新的【c1】)


*****第【31】种方法：*****
140 -> 69 -> 38 -> 50  此时，i= 6，j= 7，k= 38
过程详解：
第1步:
<将砝码2g放天平左侧>
从140g沙堆中取出69g沙子到天平左侧(作为【a1】)，71g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平右侧>
从69g沙堆中取出38g沙子到天平左侧(作为【b1】)，31g到天平右侧(作为【b2】)

第3步:

从38g沙堆中取出19g沙子到天平左侧(作为【c1】)，19g到天平右侧(作为【c2】)
将分量【b2】:31g与所得沙堆合并得50g (作新的【c1】)


*****第【32】种方法：*****
140 -> 69 -> 31 -> 90  此时，i= 6，j= 8，k= 24
过程详解：
第1步:
<将砝码2g放天平左侧>
从140g沙堆中取出69g沙子到天平左侧(作为【a1】)，71g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平左侧>
从69g沙堆中取出31g沙子到天平左侧(作为【b1】)，38g到天平右侧(作为【b2】)

第3步:
<将砝码7g放天平右侧>
从31g沙堆中取出19g沙子到天平左侧(作为【c1】)，12g到天平右侧(作为【c2】)
将分量【a2】:71g与所得沙堆合并得90g (作新的【c1】)


*****第【33】种方法：*****
140 -> 69 -> 31 -> 50  此时，i= 6，j= 8，k= 42
过程详解：
第1步:
<将砝码2g放天平左侧>
从140g沙堆中取出69g沙子到天平左侧(作为【a1】)，71g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平左侧>
从69g沙堆中取出31g沙子到天平左侧(作为【b1】)，38g到天平右侧(作为【b2】)

第3步:
<将砝码7g放天平左侧>
从31g沙堆中取出12g沙子到天平左侧(作为【c1】)，19g到天平右侧(作为【c2】)
将分量【b2】:38g与所得沙堆合并得50g (作新的【c1】)


*****第【34】种方法：*****
140 -> 69 -> 109 -> 50  此时，i= 6，j= 24，k= 12
过程详解：
第1步:
<将砝码2g放天平左侧>
从140g沙堆中取出69g沙子到天平左侧(作为【a1】)，71g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平右侧>
从69g沙堆中取出38g沙子到天平左侧(作为【b1】)，31g到天平右侧(作为【b2】)
将分量【a2】:71g与所得沙堆合并得109g (作新的【b1】)
第3步:
<将砝码9g放天平左侧>
从109g沙堆中取出50g沙子到天平左侧(作为【c1】)，59g到天平右侧(作为【c2】)



*****第【35】种方法：*****
140 -> 69 -> 109 -> 90  此时，i= 6，j= 24，k= 43
过程详解：
第1步:
<将砝码2g放天平左侧>
从140g沙堆中取出69g沙子到天平左侧(作为【a1】)，71g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平右侧>
从69g沙堆中取出38g沙子到天平左侧(作为【b1】)，31g到天平右侧(作为【b2】)
将分量【a2】:71g与所得沙堆合并得109g (作新的【b1】)
第3步:
<将砝码9g放天平右侧>
从109g沙堆中取出59g沙子到天平左侧(作为【c1】)，50g到天平右侧(作为【c2】)
将分量【b2】:31g与所得沙堆合并得90g (作新的【c1】)


*****第【36】种方法：*****
140 -> 69 -> 102 -> 50  此时，i= 6，j= 25，k= 6
过程详解：
第1步:
<将砝码2g放天平左侧>
从140g沙堆中取出69g沙子到天平左侧(作为【a1】)，71g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平左侧>
从69g沙堆中取出31g沙子到天平左侧(作为【b1】)，38g到天平右侧(作为【b2】)
将分量【a2】:71g与所得沙堆合并得102g (作新的【b1】)
第3步:
<将砝码2g放天平左侧>
从102g沙堆中取出50g沙子到天平左侧(作为【c1】)，52g到天平右侧(作为【c2】)



*****第【37】种方法：*****
140 -> 69 -> 102 -> 90  此时，i= 6，j= 25，k= 39
过程详解：
第1步:
<将砝码2g放天平左侧>
从140g沙堆中取出69g沙子到天平左侧(作为【a1】)，71g到天平右侧(作为【a2】)

第2步:
<将砝码7g放天平左侧>
从69g沙堆中取出31g沙子到天平左侧(作为【b1】)，38g到天平右侧(作为【b2】)
将分量【a2】:71g与所得沙堆合并得102g (作新的【b1】)
第3步:
<将砝码2g放天平右侧>
从102g沙堆中取出52g沙子到天平左侧(作为【c1】)，50g到天平右侧(作为【c2】)
将分量【b2】:38g与所得沙堆合并得90g (作新的【c1】)



3	思考
方法只有2种，x
