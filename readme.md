##### 1.MVVM��MVC������
 MVC��MVCģʽ����������⣬��html����view;js����controller�������û���Ӧ�õĽ�������Ӧ��view�Ĳ��������¼��ļ�����������Model�����ݽ��в��������model��view��ͬ��������model�ĸı䣬ͨ��ѡ������view���в�����;��js��ajax����Model���ӷ�������ȡ���ݣ�MVC�ǵ���ġ�
MVVM����ʵ����View��Model���Զ�ͬ����Ҳ���ǵ�Model�����Ըı�ʱ�����ǲ������Լ��ֶ�����DomԪ�أ����ı�View����ʾ�����Ǹı����Ժ�����Զ�ӦView����ʾ���Զ��ı䣬MVVM��˫��ġ�
##### 2.дһ���򵥵ĺ����ж����ͣ�

```
Object.prototype.toString.call() //�����ж�
```

##### 3.ʵ�ּ򵥵�������ͣ�

```
eval([1,2,3].join("+"))
// ��
arr.reduce((total,item)=>total+=item,0);
```

##### 4.ʵ�ּ򵥵�����ȥ�أ�
�������ݽṹ���飺

```
[...new Set([...])]��Array.from(new Set(array))(set���صĽṹ������������)
```

���������������飺
```
// ����һ��
      //���峣�� res,ֵΪһ��Map����ʵ��
      const res = new Map();
      //����arr������˺�Ľ�������Ϊһ������
      //���������ǣ����res��û��ĳ�������������������ֵΪ1
      return arr.filter((a) => !res.has(a) && res.set(a, 1))
// ��������
     //  ����2������reduce������������,reduce��һ�������Ǳ�����Ҫִ�еĺ������ڶ���            ������item�ĳ�ʼֵ
     var obj = {};
     arr = arr.reduce(function(item, next) {
     obj[next.key] ? '' : obj[next.key] = true && item.push(next);
         return item;
     }, []);
```
##### 5.��д������֪����Ԫ��ˮƽ��ֱ���У��������֣��������ã���������
- �پ��Զ�λˮƽ��ֱ����
```
<div style="
	 position: absolute;
     width: 500px;
     height: 300px;
     margin: auto;
     top: 0;
     left: 0;
     bottom: 0;
     right: 0;
     background-color: green;
     ">ˮƽ��ֱ����</div>
```
- �� ���λ��50%+margin����
```
<div style="position: relative;
     width:400px;
     height:200px;
     top: 50%;
     left: 50%;
     margin: -100px 0 0 -200px;
     background-color: red;">ˮƽ��ֱ����</div>
```
- �� ���λ��50%+translateλ��
```
<div style="position: absolute;
     width:300px;
     height:200px;
     top: 50%;
     left: 50%;
     transform: translate(-50%, -50%);
     background-color: blue;">ˮƽ��ֱ����</div>
```
- �� flex ���־���
```
<div style="display: flex;align-items: center;justify-content: center;">
    <div style="width: 100px;height: 100px;background-color: gray;">flex ����</div>
  </div>
```
##### 6.Map��Set������
Set �������������飬�ҳ�Ա��ֵ����Ψһ�ġ�
Map �����Ǽ�ֵ�Լ��ϣ��� JSON �������ƣ����� key �����������ַ����������Ƕ���
##### 7.������ʲôԭ��������ô�����
������ָһ�����µ��ĵ���ű���ͼȥ������һ�����µ���Դ����������ǹ���ġ�
- �� jsonp����
��HTML DOM��,script��ǩ����Ϳ��Է������������Դ�����������ͬԴ���Ե����ƣ�����ͨ����ҳ�涯̬����script��ǩ��
```
var script = document.createElement('script');  
script.src = "http://aa.xx.com/js/*.js";  
document.body.appendChild(script);  
```
- �� iframeʵ�ֿ���
����iframeʵ�ֵĿ���Ҫ�����������aa.xx.com,bb.xx.com�����ص㣬Ҳ��������ҳ���������ͬһ���������������綼��xxx.com������xxx.com.cn����ʹ��ͬһЭ�飨���綼�� http����ͬһ�˿ڣ����綼��80��������������ҳ����ͬʱ���document.domain���Ϳ���ʵ�ָ�ҳ�������ҳ��ĺ���
- �� ������Դ����CORS��
�������˶���CORS��֧�֣���Ҫ����ͨ������Access-Control-Allow-Origin�����еġ�����������⵽��Ӧ�����ã��Ϳ�������Ajax���п���ķ��ʡ�
- �� ʹ��HTML5��window.postMessage��������
window����������һ��window.postMessage����������細��ͨ�ţ����������������Ƿ�ͬԴ��ĿǰIE8+��FireFox��Chrome��Opera����������Ѿ�֧��window.postMessage������
- ��nginx�������
##### 8.̸һ̸CSS�ػ������/���ţ�
�ᴥ���ػ�����/���ŵĲ���
����ӡ�ɾ��Ԫ��(����+�ػ�)
������Ԫ�أ�display:none(����+�ػ�)��visibility:hidden(ֻ�ػ棬������)
���ƶ�Ԫ�أ���ı�top��left���ƶ�Ԫ�ص�����1����Ԫ����(�ػ�+����)
�ܸı��������С(����+�ػ�)
�ݸı�������������С(����+�ػ�)
�޸ı�Ԫ�ص�padding��border��margin(����+�ػ�)
�߸ı��������������ɫ��ֻ�ػ棬��������
��ı�Ԫ�صı�����ɫ��ֻ�ػ棬��������