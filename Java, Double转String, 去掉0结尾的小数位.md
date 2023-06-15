小问题：double值的小数位是0时，转String会有“.0”结尾。比如，double值是“12”，转String得到的字符串是“12.0”。如果需要去掉0结尾的小数位，应当如何解决呢？

解决方案：

```
DecimalFormat decimalFormat = new DecimalFormat("###################.###########");
System.out.println(decimalFormat.format(number));
```
　　

详细代码：

```
import java.text.DecimalFormat;
  
public class Test {
    public static void main(String[] args){
        double number = 12;
         
        System.out.println(number);                         //12.0
         
        System.out.println(Double.toString(number));        //12.0
  
        DecimalFormat decimalFormat = new DecimalFormat("###################.###########");
        System.out.println(decimalFormat.format(number));   //12
    }
}
```
　　
