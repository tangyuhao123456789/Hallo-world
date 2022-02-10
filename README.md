


#包括<iostream>
#include <流>
#包括<cstdio>
#包括<字符串>

使用命名空间 std;

// 表达式
字符串公式;
const int MAXL = 100 + 5;
// 表达式中元素（符号&数字）的数量
int cnt = 0;
中缀表达式
字符串中缀[MAXL];
后缀表达式
字符串后缀[MAXL];
临时栈
字符堆栈1[最大值];
字符串堆栈2[最大值];
双层3[最大];

错误处理
int 错误框 = 0;

const int ILLEGAL_CHARACTER = 1;
const int BRACKET_ERROR = 2;
const int FORMULA_TOO_LONG = 3;

string errorstr[5] = { "NO ERROR or UNKNOWN ERROR"， "ILLEGAL_CHARACTER"， "BRACKET_ERROR"，
	"FORMULA_IS_TOO_LONG"
};

判断为数字或运算符
内联布尔is_num（字符 c）
{
	return （（c >= '0' &c <= '9'） || c == '.');
}

内联布尔is_saf（字符 c）
{
	返回 （c == '+' || c == '-' || c == '*' || c == '/' || c == '（' || c ==')');
}

内联布尔is_blank（字符 c）
{
	返回 c ==' ';
}

// 运算符优先级（优先级）
int get_plvl（char c）
{
	开关 （c）
	{
	大小写 "（"：
		返回 0;
		破;
	案例"+"：
		返回 1;
		破;
	大小写"-"：
		返回 1;
		破;
	大小写"*"：
		返回 2;
		破;
	案例"/"：
		返回 2;
		破;
	}
}

初始化
void init();
读取并储存
空隙输入();
将字符串转为double
双转（字符串和数字）;
识别运算符进行运算
double cal（double &num1， double &num2， char &c）;
// 程序主体
双重计算();

int main（void)
{
cout << "-----控制台计算器-----\n" "----------by-QingFLS\n" "\n";
	初始化();
	而 （1)
	{
		输入();
		如果 （！错误框）
		{
cout <<公式 << " = \n" <<计算（） << endl;
		}
		还
cout << "错误!!!\n" <<公式 << endl << errorstr[errorbox] << endl;

		初始化();
	}
	返回 0;
}

初始化
void init()
{
公式。清楚();
	// 表达式中元素（符号&数字）的数量
cnt = 0;
	中缀表达式
	for （int i = 0; i ！= MAXL; i++）
中缀[i].清楚();
	后缀表达式
	for （int i = 0; i ！= MAXL; i++）
后缀[i].。清楚();
	临时栈
	for （int i = 0; i ！= MAXL; i++）
stack1[i] = 0;
	for （int i = 0; i ！= MAXL; i++）
stack2[i].清楚();
	for （int i = 0; i ！= MAXL; i++）
stack3[i] = 0.0;
	错误处理
错误框 = 0;
}

空隙输入()
{
	/* 从文件读取 ifstream fin（"in.txt"）;getline（fin， formula， '\n'）;
fin.close（）;*/
cout <<"请输入您的公式：\n\n";
	getline（cin， formula， '\n');

	第一步简单错误处理
	int brk = 0;
	for （int i = 0; i ！= formula.长度（）;i++）
	{
		存在非法字符
		如果 （！（is_num（式[i]） ||is_saf（式[i]）||is_blank（式[i]））
		{
错误框 = ILLEGAL_CHARACTER;
			返回;
		}

		括号不匹配
		if （formula[i] == '（' || formula[i] ==')')
			断续器++;
	}

	if （brk % 2 ！= 0)
	{
错误框 = BRACKET_ERROR;
		返回;
	}

	// 若第一步无错误
	// 将表达式各元素分离，存为中缀表达式
	for (int i = 0; i < formula.length() && cnt < MAXL;)
	{
		// 跳过空格
		if (formula[i] == ' ')
		{
			i++;
			continue;
		}
		// 存运算符
		if (is_saf(formula[i]))
		{
			infix[cnt] = formula[i];
			i++;
		}
		// 存数字
		else
			for (int k = 0; i < formula.length() && is_num(formula[i]); k++)
			{
				infix[cnt] += formula[i];
				i++;
			}
cnt++;
	}

	// 处理负数（在负号前插入0）
	int p = 1;
	若首位为负号
	if （infix[0][0] == '-')
	{
cnt++;
		for （int i = cnt - 1; i ！= 0; i--）
infix[i] = infix[i - 1];
中缀[0] = "0";
	}
	// 在表达式其它地方寻找负号
	而 （p ！= cnt）
	{
		if （infix[p][0] == '-' && infix[p - 1][0] == '(')
		{
cnt++;
			for （int i = cnt - 1; i ！= p; i--）
infix[i] = infix[i - 1];
中缀[p] = "0";
		}
p++;
	}
	/* 
Test，cnt为表达式中元素个数 for（int t=0;t！=cnt;t++）
cout<<infix[t]<<endl;cout<<"Cnt="<<cnt<<endl;*/

	第二步简单错误处理
	如果表达式元素数量超出范围
	如果 （cnt > 最大值 - 5)
	{
错误框 = FORMULA_TOO_LONG;
		返回;
	}
}

双重计算()
{
	// 将中缀表达式转为后缀表达式
	int top = 0;后缀栈顶
	int stk = 0;堆栈1栈顶

	for （int i = 0; i ！= cnt; i++）
	{
		if （is_num（infix[i][0]))
		{
后缀[top++] = 中缀[i];
		}
		还
			开关 （中缀[i][0])
			{
			大小写 "（"：
stack1[stk++] ='(';
				破;
			大小写 "）"：
				而 （stk > 0)
					if （stack1[stk - 1] ！='(')
					{
stk--;
后缀[top++] = stack1[stk];
					}
					还
					{
stk--;
stack1[stk] = '\0';
						破;
					}
				破;
			默认值：
				while （stk > 0 && get_plvl（infix[i][0]） <= get_plvl（stack1[stk - 1]))
				{
后缀[顶部] = 堆栈 1[stk - 1];
顶部++;
stk--;
				}
stack1[stk++] = infix[i][0];
				破;
			}
	}

	对于 （;stk ！= 0;stk--）
后缀[top++] = stack1[stk - 1];

	// 利用后缀表达式进行栈运算
	/* 
	   //Test for(int t = 0; t != top; t++) cout<<suffix[t]<<endl;
	   cout<<"Top="<<top<<endl; */

	// 将string存储的数字转为double
	// 有较大精度损失，留待以后改进

stk = 0;堆栈3栈顶
	for （int i = 0; i ！= top; i++）
	{
		if （is_num（后缀[i][0]))
		{
			将字符串转为double
stack3[stk++] = trans（后缀[i]）;
		}
		还
		{
stk -= 2;
stack3[stk] = cal（stack3[stk]， stack3[stk + 1]， 后缀[i][0]);
stk++;
		}
	}
stk = 0;

	返回堆栈3[0];
}

双反转（字符串和数字）
{
	双精度结果 = 0.0;
	记录小数点出现
	整数点 = -1;

	for （int j = 0; j ！= num.length（）; j++）
	{
		if （num[j] == '.')
		{
点 = j;
			继续;
		}
结果 *= 10;
结果 += （数字[j] - 48);
	}
	for （int k = 0; dot ！= -1 && k ！= num.length（） - dot - 1; k++）
结果 /= 10;

	返回结果;
}

双 cal（双 &num1， 双 &num2， char &c）
{
	开关 （c）
	{
	案例"+"：
		返回 （num1 + num2）;
		破;
	大小写"-"：
		返回 （num1 - num2）;
		破;
	大小写"*"：
		返回 （num1 * num2）;
		破;
	案例"/"：
		返回 （num1 / num2）;
		破;
	默认值：
		破;
	}
}


e
